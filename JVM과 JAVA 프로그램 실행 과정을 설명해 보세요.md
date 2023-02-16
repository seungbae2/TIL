# JVM과 JAVA 프로그램 실행 과정을 설명해 보세요

> JAVA 프로그램은 JVM 상에서 실행되므로 JVM과 JAVA 프로그램의 구조/실행 방식을 잘 이해하고 있어야 보다 효율적인 프로그램 작성이 가능하므로 이와 관련된 지식을 판단하고자 함
> 

- JVM이란 JAVA Virtual Machine 의 약자로 자바프로그램을 자바 API를 기반으로 실행하는 역할을 함
- JAVA 프로그램 실행 과정은
    - 프로그램이 실행되면 JVM이 OS로부터 해당 프로그램이 필요로 하는 메모리를 할당받고
    - 자바 바이트코드로 변환된(.class) 파일을 class로더를 통해 JVM에 로딩한다
    - 로딩된 class 파일은 execution engine을 통해 해석되고 실행된다
    - 필요시 garbage collecion을 수행해서 불필요하게 할당된 메모리를 해제한다