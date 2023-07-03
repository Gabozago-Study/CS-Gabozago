# Dynamic Programming

### Dynamic Programming (동적계획법)
- 큰 문제를 작은 하위 문제로 나누어 해결하는 알고리즘 설계 기법
- 중복되는 하위 문제를 효율적으로 해결하여 전체 문제를 효율적으로 해결하는 방법을 제공 
- 최적화 문제를 해결하는 데 주로 사용되며, 최적 부분 구조와 중복 부분 문제의 특징을 가진 문제에 적용된다

###  Dynamic Programming의 특징
- Overlapping Subproblems (중복 부분 문제)
	- Dynamic Programming은 큰 문제를 작은 하위 문제로 분할하는데, 이 때 하위 문제가 여러 번 반복되는 경우가 발생 할 수 있다. Dynamic Programming은 이러한 중복 부분 문제를 해결하여 중복 계산을 피하고, 계산 속도를 대폭 향상시킨다.

- Memoization 
	- 중복 부분 문제를 해결하기 위해 이전에 계산한 결과를 저장하고 재사용하는 메모이제이션 기법이 사용된다. 이를 통해 중복 계산을 피하고 실행 시간을 줄일 수 있으며 메모이제이션은 일반적으로 배열 또는 해시 테이블을 사용하여 결과를 저장한다.

- Bottom-up or Top-down Approach
	- Dynamic Programming은 일반적으로 Bottom-up 또는 Top-down 접근 방식을 사용한다. Bottom-up 접근 방식은 작은 하위 문제부터 시작하여 차례대로 큰 문제까지 해결하는 반면, Top-down 접근 방식은 큰 문제를 해결하는 동안 필요한 하위 문제를 재귀적으로 호출하여 해결합니다.

