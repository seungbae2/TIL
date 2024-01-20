# Version Catalog

[Gradle 버전 카탈로그](https://docs.gradle.org/current/userguide/platforms.html)를 사용하면 확장 가능한 방식으로 종속 항목 및 플러그인을 추가하고 유지할 수 있다.

Gradle 버전 카탈로그를 사용하면 [여러 모듈](https://developer.android.com/topic/modularization?hl=ko)이 있을 때 종속 항목과 플러그인을 더 쉽게 관리할 수 있다.

버전이 바뀔 때마다 전체가 빌드되는 BuildSrc 의 문제를 해결할 수 있다.

종속 항목을 업그레이드해야 할 때마다 종속 항목의 이름과 버전을 개별 빌드 파일에 하드코딩하고 각 항목을 업데이트하는 대신, 종속 항목의 중앙 *버전 카탈로그*를 생성하면 다양한 모듈에서 Android 스튜디오 지원을 활용해 유형 안전 방식으로 이를 참조할 수 있습니다.