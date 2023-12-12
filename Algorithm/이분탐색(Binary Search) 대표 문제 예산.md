# 이분탐색(Binary Search) 대표 문제: 예산

[프로그래머스](https://school.programmers.co.kr/learn/courses/10302/lessons/62949)

어떤 주어진 데이터에서 원하는 특정 데이터를 찾는것을 탐색이라 한다

모든 값을 순회하는덴 시간이 너무 오래 걸린다

최소값과 최대값이 주어진다

이미 데이터가 정렬되어 있는 상태

이분탐색을 생각해볼 수 있다

중간값을 상한선으로 했을 때 총합이 예산을 넘는지 안넘는지 확인

예산 초과하지 않았다면 다시 상향 조정해서 줄여간다

예산을 초과한다면 다시 줄인다

최대값과 최소값이 같아질때까지 반복

```java
import java.util.stream.*;

class Solution {
	public int solution(int[] budgets, int M) {
		int min = 0;
		int max = IntStream.of(budgets).max().orElse(0);
		
		int answer = 0;
		while(min <= max) {
			final int mid = (min + max) / 2;
			
			int sum = IntStream.of(budgets)
						.map(b-> Math.min(b, mid))
						.sum();

			if(sum <= M) {
				min = mid + 1;
				answer = mid;
			} else {
				max = mid - 1;
			}
		}

		return answer;
	}
}
```

좋은 프로그램을 만드는 방법

1. 당면한 문제를 해결한다
2. 좋은 코드가 되도록 계속 리팩토링 한다