# ViewModel이 화면 회전에도 데이터를 유지할 수 있는 이유

안드로이드에서 구성변경(Configuration Change)가 일어날 때 ViewModel 객체는 Activity가 재생성 되더라도 파괴되지 않고 객체가 유지

Activity Destroy → ViewModel onCleared()

ViewModel은 Activity의 종료가 구성변경과 같은 재생성에 의한 종료인지 finish()를 통한 종료인지 어떻게 알 수 있을까?

ViewModel에서 onCleared() 호출되는 함수

```java
public abstract class ViewModel { 
    @SuppressWarnings("WeakerAccess")
    protected void onCleared() {
    }

    @MainThread
    final void clear() {
      ///..
      onCleared();
    }
}
```

ViewModelStore 객체에서 ViewModeld의 clear() 호출 

```java
public class ViewModelStore {

    private final HashMap<String, ViewModel> mMap = new HashMap<>();

    final void put(String key, ViewModel viewModel) {
        ViewModel oldViewModel = mMap.put(key, viewModel);
        if (oldViewModel != null) {
            oldViewModel.onCleared();
        }
    }

    final ViewModel get(String key) {
        return mMap.get(key);
    }

    Set<String> keys() {
        return new HashSet<>(mMap.keySet());
    }

    /**
     *  Clears internal storage and notifies ViewModels that they are no longer used.
     */
    public final void clear() {
        for (ViewModel vm : mMap.values()) {
            vm.clear();
        }
        mMap.clear();
    }
}
```

ViewModelStore는 ViewModel들을 저장하기 위한 클래스

ViewModelStore는 Owner(Activity or Fragment)에 의해 구성변경이 되어도 인스턴스를 유지해야 한다

만약 ViewModelStoreOwner가 완전히 파괴되고 재생성되지 않는다면 clear()를 호출해서 더이상 ViewModel이 사용되지 않는다는 사실을 Activity나 Fragment에 알려야 한다

ComponentActivity에서 ViewModelStore clear() → ViewModel clear() 호출

```java
public ComponentActivity() {
  getLifecycle().addObserver(new LifecycleEventObserver() {
      @Override
      public void onStateChanged(
        @NonNull LifecycleOwner source,
        @NonNull Lifecycle.Event event
      ) {
          if (event == Lifecycle.Event.ON_DESTROY) {
              // Clear out the available context
              mContextAwareHelper.clearAvailableContext();
              // And clear the ViewModelStore
              if (!isChangingConfigurations()) {
                  getViewModelStore().clear();
              }
          }
      }
  });
}
```

ComponentActivity 에서는 LifecycleEventObserver를 관찰자로 등록하고 onDestroy 와  !isChangingConfigurations()가 모두 만졸할 경우 ViewModelStore의 clear()가 호출되어 ViewModel까지 전달되는 것을 볼 수 있다

```java
public class Activity {
  boolean mChangingConfigurations = false;
  
  public boolean isChangingConfigurations() {
        return mChangingConfigurations;
  }
}
```

isChangingConfigurations() 는 Acitivty 클래스의 내부 멤버변수를 리턴해주는 함수

mChangingConfigurations를 변경하는 곳: ActivityThread

```java
@Override
public void handleRelaunchActivity(
  ActivityClientRecord tmp,
  PendingTransactionActions pendingActions
) {
  ActivityClientRecord r = mActivities.get(tmp.token);
  if (DEBUG_CONFIGURATION) Slog.v(TAG, "Handling relaunch of " + r);
  if (r == null) {
    return;
  }

  r.activity.mConfigChangeFlags |= configChanges;
  r.mPreserveWindow = tmp.mPreserveWindow;

  r.activity.mChangingConfigurations = true;
}
```

ViewModeld의 생성도 결국 Activity에서 이루어지는데 Activity가 완전히 파괴되고 만들어질 때 ViewModel의 인스턴스를 어떻게 유지할까? → ViewModelStoreOwner에 해답이 있음

```java
public interface ViewModelStoreOwner {
    @NonNull
    ViewModelStore getViewModelStore();
}
```

ViewModelStoreOwner 인터페이스 주석 설명을 보면 이 인터페이스 구현체의 책임은 구성 변경중에도 ViewModelStore를 유지하고 이 범위가 파괴될 때 `ViewModelStore.clear()`
를 호출하는 것이라고 적혀있음

ViewModelStoreOwner의 구현체 ComponentActivity

```java
@NonNull
@Override
public ViewModelStore getViewModelStore() {
    if (getApplication() == null) {
        throw new IllegalStateException("Your activity is not yet attached to the "
                + "Application instance. You can't request ViewModel before onCreate call.");
    }    //This is true when invoked for the first time
    if (mViewModelStore == null) {
        NonConfigurationInstances nc =
                (NonConfigurationInstances) getLastNonConfigurationInstance();
        if (nc != null) {
            // Restore the ViewModelStore from NonConfigurationInstances
            mViewModelStore = nc.viewModelStore;
        }
        if (mViewModelStore == null) {
            mViewModelStore = new ViewModelStore();
        }
    }
    return mViewModelStore;
}
```

getLastNonConfigurationInstance() 를 호출 NonConfigurationInstances라는 클래스를 캐스팅해서 ComponentActivity의 ViewModelStore멤버변수로 할당

Activity가 구성변경에 의해 재생성될 때 ComponentActivity의 NonConfigurationInstances 클래스는 이전 ViewModelState의 인스턴스를 포함하고 있다

Activity가 처음 생성될 때 NonConfigurationInstances 는 null을 반환하고 그런 경우에는 ViewModelStore를 새로 생성

```java
//Activity.java
@Nullable
public Object getLastNonConfigurationInstance() {
  return mLastNonConfigurationInstances != null
    ? mLastNonConfigurationInstances.activity : null;
}

//ComponentActivity.java
@Override
@Nullable
@SuppressWarnings("deprecation")
public final Object onRetainNonConfigurationInstance() {
  // Maintain backward compatibility.
  Object custom = onRetainCustomNonConfigurationInstance();

  ViewModelStore viewModelStore = mViewModelStore;
  if (viewModelStore == null) {
    // No one called getViewModelStore(), so see if there was an existing
    // ViewModelStore from our last NonConfigurationInstance
    NonConfigurationInstances nc =
      (NonConfigurationInstances) getLastNonConfigurationInstance();
    if (nc != null) {
      viewModelStore = nc.viewModelStore;
    }
  }

  if (viewModelStore == null && custom == null) {
    return null;
  }

  NonConfigurationInstances nci = new NonConfigurationInstances();
  nci.custom = custom;
  nci.viewModelStore = viewModelStore;
  return nci;
}
```

Activity 구성변경 → ComponentActivity onRetainNonConfigurationInstance() → getLastNonConfigurationInstance() →Activity의 mLastNonConfigurationInstances.activity를 반환

이 객체는 안드로이드 시스템에서 재생성된 후의 액티비티를 전달한 것

Activity가 재생성 후에 Activity.java클래스에서 mLastNonConfigurationInstances 객체는 attach()에서 lastNonConfigurationInstances를 전달받아 mLastNonConfigurationInstances에 할당