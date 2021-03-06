1. 그리디 알고리즘이란? 
    - 단순하지만 강력한 문제 해결 방법
    - 현재 상황에서 지금 당장 좋은 것만 고르는 방법
    - '가장 큰 순서대로' , ' 가장 작은 순서대로' 같은 기준을 제시
    - 대체로 정렬 알고리즘과 짝을 이뤄 출시
2. 예시
    1. **거스름돈** 

        ```
        1. 카운터에는 거스름돈으로 사용할 500원, 100원, 50원, 10원 짜리 동전이 무한히 존재
        2. 손님에게 거슬러 줘야 할 돈이 N원 일떄 거슬러 줘야 할 동전의 최소 개수를 구하라.
        ```

        >'가장 큰 화폐 단위부터' 돈을 거슬러 주는 것 

        ```python
        n = 1260
        count = 0

        list = [500, 100, 50, 10]

        for coin in list 
        	count += n // coin # 해당 화폐로 거슬러 줄 수 있는 동전의 갯수 세기
        	n %= coin 

        print(count)
        ```

    2. **큰 수의 법칙** 

        ```
        입력 조건
        1. 첫째 줄에 N(2<= N <= 1000), M(1<= M <= 10,000), K(1<= K <= 10,000)
        	 의 자연수가 주어지며, 각 자연수는 공백으로 구분한다. 
        2. 둘째 줄에 N개의 자연수가 주어진다. 각 자연수는 공백으로 구분한다. 단, 각각의 자연수는 1이상
           10,000이하의 수로 주어진다
        3. 입력으로 주어지는 K는 항상 M보다 작거나 같다.

        입력 예시 
        5 8 3
        2 4 5 4 6 

        출력 예시
        46
        ```

       > 1. 입력값 중 가장 큰 수와 두 번째로 큰 수만 저장하면 된다.
       >2. 가장 큰 수를 K번 더하고 두 번째로 큰수를 한 번 더하는 연산을 반복하면 된다.

        ```python
        n, m, k = map(int, input().split()) # 공백으로 구분 하여 입력

        data = list(map(int, input().split())) 

        data.sort()
        first = data[n-1] # 가장 큰수
        second = data[n-2] # 두 번째로 큰수

        result = 0
        1
        while True:
          for i in range(k): # 큰 수를 K번 더하기 
            if m == 0: # m이 0이면 반복문 break
              break
            result += first 
            m -= 1 # 더할 때마다 m 감소 
          if m == 0:
            break
          result += second # 두 번째로 큰 수 한 번 더하기
          m -= 1 # 더할 때마다 m 감소
        print(result) # 결과 출력
        ```

        위 코드는 M이 10,000이하일때 해결 가능하지만 
        100억이상 처럼 커진다면 시관 초과 판정을받음 
        ⇒ 반복되는 수열에 대해서 파악해야 한다 

        예시 2 4 5 4 6 
        1. 가장 큰 수 : 6
        2. 두 번째로 큰 수: 5
        - M = 8, K=3 이라면 
        (6+6+6+5) + (6+6+6+5) = 46
        수열 {6,6,6,5} 가 반복 
        ⇒ **수열의 길이는 (K+1), 수열의 반복 횟수는 M / (K+1) 값** **,마지막 * K** 
        ⇒ M이 나누어 떨어지지 않을 경우 고려 ⇒ M % (K+1) 
        결론: int( M / (K+1)) * K + M % (K+1)

        ```python
        n, m, k = map(int, input().split()) # 공백으로 구분 하여 입력

        data = list(map(int, input().split())) 

        data.sort()
        first = data[n-1] # 가장 큰수
        second = data[n-2] # 두 번째로 큰수

        # 가장 큰 수가 더해지는 횟수 개산 => 
        count = int(m/(k+1)) * k + m % (k + 1)
        #count += m % (k + 1)

        result = 0
        result += (count) * first
        result += (m-count) * second

        print(result))
        ```

    3. **숫자 카드 게임**

        ```
        입력 조건
        1. 첫째 줄에 숫자 카드들이 놓인 행의 개수 N과 열의 개수 M이 공백을 기준으로 하여 각각 자연수로 주어진다
        (1<=N, M <=100)
        2. 둘째 줄부터 N개의 줄에 걸쳐 각 카드에 적힌 숫자가 주어진다. 각 숫자는 1 이상 10,000이하의 자연수 이다.

        출력 조건 
        1. 첫째 줄에 게임의 룰에 맞게 선택한 카드에 적힌 숫자를 출력한다.

        입력 예시 1
        3 3
        3 1 2
        4 1 4
        2 2 2
        출력 예시 1
        2

        입력 예시 2
        2 4
        7 3 1 8
        3 3 3 4
        출력 예시 2
        3
        ```

        >**각 행마다 가장 작은 수를 찾은 뒤에 그 수 중에서 가장 큰 수**를 찾는 것

        ```python
        # min() 함수 이용 답안
        n, m = map(int, input().split())

        result = 0

        for i in range(n):
          data = list(map(int,input().split()))
          min_value = min(data)
          result = max(result, min_value)

        print(result);

        # 2중 for문
        n, m = map(int, input().split())

        result = 0

        for i in range(n):
        	data = list(map(int,input().split()))
        	# 현재 줄에서 가장 작은 수 찾기
        	min_value = 10001 
        	for a in data: 
        		min_value = min(min_value, a)
        	# 가장 작은 수들 중에서 가장 큰 수 찾기 
        	result = max(result, min_value)
        print(result)
        ```

    4. **1이 될때 까지**

        ```
        입력 조건
        1. 첫째 줄에 N(2<=N <= 100,000)과 K(2<=K<=100,000)가 공백으로 구분되며 각각 자연수로 주어진다.
        	 이때 입력으로 주어지는 N은 항상 K보다 크거나 같다
        출력 조건
        1. 첫째 줄에 N이 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 횟수의 최솟값을 출력한다.

        입력 예시
        25 5
        출력 예시 
        2
        ```

        >N이 K의 배수가 될 때까지 1씩 빼고 N을 K로 나누기 

        ```python
        n, k = map(int, input().split())

        result = 0

        while True:
            # N이 K로 나누어 떨어지는 수가 될 때까지만 1씩 빼기
            target = (n // k) * k
            print(target)
            result += (n - target)
            print(result)
            n = target
            # N이 K보다 작을 때 (더 이상 나눌 수 없을 때) 반복문 탈출
            if n < k:
                break
            # K로 나누기
            result += 1
            n //= k

        # 마지막으로 남은 수에 대하여 1씩 빼기
        result += (n - 1)
        print(result)
        ```