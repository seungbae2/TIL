# 시뮬레이션(Simulation) 대표 문제: 숫자 게임

[프로그래머스](https://school.programmers.co.kr/learn/courses/10302/lessons/62947)

B팀의 경우의 수를 확인 후 원하는 값을 찾으면 탐색법

B가 최대 승점으로 이기는 조건 

특정 상황을 재현 → 시뮬레이션

B가 근소한 차이로 A를 이기는 것이 최대 승점

B의 작은 값부터 시작해서 A를 이길 수 있는 값들을 제거해 가면서 승점을 구하면 쉽게 찾을 수 있다

```java
import java.util.*;

class Solution {
	public int solution(int[] A, int[] B) {
		Arrays.sort(A);
		Arrays.sort(B);
		int index = B.length - 1;

		int answer = 0;
		for(int i=A.length-1; i>=0; i--) {
			if(A[i] < B[index]) {
				index--;
				answer++;
			}
		}

		return answer;
	}
}
```