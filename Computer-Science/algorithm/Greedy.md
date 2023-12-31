
## Greedy Algoritm

`Greedy Algorithm(탐욕법)`은 현재 상황에서 **지금 당장 좋은 것**만을 고르는 방법의 설계 기법을 말한다. 즉, 최적해를 구할 때 사용되는 방법인데 모든 경우의 수를 고려하는 것이 아닌, 해를 구하는 과정에서 그 순간에 최적인 경우만을 골라 최적해를 구하는 방법이다. 

`Greedy Algoritm`은 최적 부분 구조에서도 탐욕 선택 속성을 가진 방법론이고, 이 경우에 강점이 있다. 위의 이야기를 해석하자면 문제를 부분으로 분할하여 해결하되, 지금의 선택이 이후의 선택과 연관이 있지 않아야 한다. 

그래서 항상 이 방법으로 문제를 해결하기 위해서는 정당한가에 대한 고민을 거쳐야만 한다. 정말 지금 내 앞에 놓여져 있는 문제가 **탐욕 선택 속성**을 가질 수 있는가를 확인해야 한다.

### Greedy 예제

[거스름돈 (Bronze 2)](https://www.acmicpc.net/problem/5585)

**문제**

	타로는 자주 JOI잡화점에서 물건을 산다. JOI잡화점에는 잔돈으로 500엔, 100엔, 50엔, 10엔, 5엔, 1엔이 충분히 있고, 언제나 거스름돈 개수가 가장 적게 잔돈을 준다. 타로가 JOI잡화점에서 물건을 사고 카운터에서 1000엔 지폐를 한장 냈을 때, 받을 잔돈에 포함된 잔돈의 개수를 구하는 프로그램을 작성하시오.

**입력**

	 입력은 한줄로 이루어져있고, 타로가 지불할 돈(1 이상 1000미만의 정수) 1개가 쓰여져있다.

**출력**

	 제출할 출력 파일은 1행으로만 되어 있다. 잔돈에 포함된 매수를 출력하시오.

**예제 입력 1**

	 380

**예제 출력 1**

	 4

**예제 입력 2**

	 1

**예제 출력 2**

	 15

이 경우에 `Greedy Algorithm`을 이용하여 문제를 푼다면, 가능한 가장 작은 화폐 단위부터 돈을 거슬러 주는 방법으로 풀이할 수 있다. 만약 내가 잔돈 700원을 받야아 한다고 가정하면, 가장 큰 단위인 500원부터 거슬러 받으며 거스름돈의 개수를 줄이는 방법이다.

#### 예제 풀이

```python
import sys  
  
N = int(sys.stdin.readline().rstrip())

money = 1000 - N  
coins = [500, 100, 50, 10, 5, 1]  
result = 0  
  
for coin in coins:  
    result += money // coin  
    money %= coin  
  
print(result)
```

위와 같은 방법으로 간단하게 해결 할 수 있다. 하지만 이 방법이 반드시 최적해를 얻을 수 있다는 이유는 무엇일지 생각을 해봐야 한다. 지금 당장 큰 수를 고르는 선택이 이후에 영향을 미치지 않는다는 근거는 무엇인가?

이에 대한 근거는 큰 동전이 항상 작은 동전의 배수가 된다는 것이다. 500원을 100원을 가지고 조합을 할 수 있고, 50원을 가지고도 조합을 할 수 있다. 다른 동전도 마찬가지다. 이런 근거가 있기 때문에 위 방법의 정당성이 생긴다.


### 풀어보면 좋은 예제

[잃어버린 괄호 (Silver 2)](https://www.acmicpc.net/problem/1541)
