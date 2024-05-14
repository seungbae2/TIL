# PullToRefresh

Compose Material3 버전 1.3.0-alpha06 에서 새로운 pull-to-refresh api 추가

- Dp단위 대신 소수 값을 사용하도록 PullToRefreshState 를 단순화했다.
- isRefreshing상태는 PullToRefreshState대신 사용자가 제어한다.
- 중첩 스크롤 연결을 PullToRefreshState에서 분리했다. 새 PullToRefreshBox 또는 Modifier.pullToRefresh에 의해 처리된다.

새로 추가된 PullToRefreshBox

```kotlin
@Composable
@ExperimentalMaterial3Api
fun PullToRefreshBox(
    isRefreshing: Boolean,
    onRefresh: () -> Unit,
    modifier: Modifier = Modifier,
    state: PullToRefreshState = rememberPullToRefreshState(),
    indicator: @Composable BoxScope.() -> Unit = {
        Indicator(
            modifier = Modifier.align(Alignment.TopCenter),
            isRefreshing = isRefreshing,
            state = state
        )
    },
    content: @Composable BoxScope.() -> Unit
): Unit
```

- PullToRefreshBox는 content로 스크롤 가능한 레이아웃을 넣어줘야 한다. LazyColumn 같은 거나 아니면 Modifier에서 verticalScroll(rememberScrollState()) 를 넣어주면 된다.
- 기본적으로  PullToRefreshDefaults.Indicator를 Indicator로 사용한다. 커스텀을 원하면은 indicator에 커스텀한 Indicator를 넣어주면 된다.