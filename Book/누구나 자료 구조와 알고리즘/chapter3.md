# 3장. 빅 오 표기법

선형 검색의 효율성을 정량화하는 효과적인 방법은 

- N개의 원소가 있을 때 선형 검색에 N단계가 필요하다고 표현하는 것이다.
- 하지만 이 방법은 다소 장황하다.

**빅 오 표기법**

- 컴퓨터 과학자들은 시간 복잡도를 쉽게 소통할 목적으로 자료 구조와 알고리즘의 효율성을 간결하고 일관된 언어로 설명하기 위한 수학적 개념을 차용
- 이런 개념을 형식화한 표현을 빅 오 표기법이라 함
- 빅 오 표기법으로 주어진 알고리즘의 효율성을 쉽게 분류하고 이해할 수 있음
- 일관되고 간결한 방법으로 어떤 알고리즘이든 분석 가능

# 3.1 빅 오: 원소가 N개일 때 몇 단계가 필요할까?

빅 오는 특정 방식으로 알고리즘에 필요한 단계 수를 고려함으로써 일관성을 유지한다.

선형 검색 알고리즘을 빅 오로 나타내 보자. 최악의 경우 선형 검색에는 배열의 원소 수만큼의 단계가 필요하다. 빅 오 표기법으로 이를 표현하는 적절한 방법은 다음과 같다.

$$
O(N)
$$

- "빅 오 N" 이라고 발음한다.
- "차수 N" 이라고도 부른다.

위 표기는 "핵심 질문"에 대한 답을 나타낸다. 여기서 핵심 질문이란

- "데이터 원소가 N개일 때 알고리즘에 몇 단계가 필요할까?"이다.
- 이것이 빅 오의 정의이다.

핵심 질문에 대한 답은 빅 오 표현의 괄호 안에 들어 있다.

- O(N)은 알고리즘에 N단계가 필요하다는 답을 나타낸다.

빅 오 표기법으로 선형 검색의 시간 복잡도를 표현하는 사고 과정

- 핵심 질문: 배열에 원소가 N개일 때 선형 검색에 몇 단계가 필요할까?
- 답: 선형 검색에 N단계가 필요하므로 O(N)으로 표현한다.
- 빅 오 표기법으로 O(N)인 알고리즘을 선형 시간(linear time)을 갖는 알고리즘이라고도 부른다.

일반적인 배열 읽기에 필요한 단계 수는 배열의 크기와 상관 없이 단 한 단계이다. 빅 오로 이것을 어떻게 표현할까?

- 핵심 질문: 데이터 원소가 N개일 때 배열에서 읽기에 몇 단계가 필요할까?
- 답: 읽기에는 딱 한 단계가 필요하므로 O(1)이라 표현한다. "오 1"이라고 읽는다.
- N에 대해 질문해지만 답은 N과 무관하다. 바꿔 말하면 배열에 원소가 몇 개든 배열에서 읽기는 항상 한 단계면 된다.

O(1)은 "가장 빠른" 알고리즘 유형으로 분류한다.

- 데이터가 늘어나도 O(1) 알고리즘의 단계 수는 증가하지 않는다.
- N이 얼마든 항상 상수 단계만 필요하다.
- 그래서 O(1) 알고리즘을 상수 시간(constant time)을 갖는 알고리즘이라고도 표현한다.

# 3.2 빅 오의 본질

빅 오 표기법은 머릿속에 새겼던 핵심 질문, 즉 데이터 원소가 N개일 때 알고리즘에 몇 단계가 필요한가에 대한 답이다.

데이터가 몇 개든 항상 3단계가 걸리는 알고리즘이 있다고 가정하자. 즉 원소가 N개일 때 알고리즘에 항상 3단계가 필요하다. 이를 빅 오로 어떻게 표현할까?

- 지금까지 배운 지식에 따라 O(3)이라고 답할 것이다.
- 하지만 실제로는 O(1)이다.

그 이유를 알려면 빅 오를 더 깊이 이해해야 한다.

- 빅 오는 데이터 원소 N개에 대한 알고리즘의 단계 수를 나타낸다.
- 빅 오의 본질이란 빅 오가 진정으로 의미하는 것, 즉 데이터가 늘어날 때 알고리즘의 성능이 어떻게 바뀌는지를 뜻한다.
- 빅 오는 단순히 알고리즘에 필요한 단계 수만 알려주지 않는다. 데이터가 늘어날 때 단계 수가 어떻게 증가하는지 설명한다.

이런 관점에서 알고리즘이 O(1)이든 O(3)이든 중요하지 않다. 두 알고리즘 모두 데이터 증가에 영향을 받지 않는, 즉 단계 수가 변하지 않는 유형이므로 본질적으로 같은 알고리즘 유형이다. 둘 다 데이터에 관계 없이 단계 수가 일정한 알고리즘이므로 둘을 구분하지 않는다.

반면 O(N) 알고리즘은 유형이 다르다.

- 데이터 증가가 성능에 영향을 미친다.
- 데이터가 늘어날 때 정확히 그 데이터에 비례해 단계 수가 증가하는 알고리즘 유형이다.
- 알고리즘의 효율성과 데이터가 비례 관계이다.

O(N)과 O(1) 알고리즘 유형의 그래프는 다음과 같다.

![](https://images.velog.io/images/realryankim/post/29965e56-046a-4fd6-86ff-6d94c90e96fd/big-o-chart-tutorial-bazar-aymptotic-notations-1.png)

O(N)

- 완벽한 대각선
- 데이터가 하나 추가될 때마다 알고리즘이 한 단계씩 추가됨
- 데이터가 많아질수록 알고리즘에 필요한 단계 수도 증가

O(1)

- 완벽한 수평선
- 데이터가 얼마나 많든 상관 없이 단계 수가 일정

## 3.2.1 빅 오의 본질 더 파고들기

데이터 크기에 상관 없이 항상 100단계가 걸리는 상수 시간 알고리즘이 있다고 가정하자. 이 알고리즘은 O(N)인 알고리즘보다 성능이 우수할까?

- 원소가 100개 이하인 데이터 세트에서는 100단계가 걸리는 O(1) 알고리즘보다 O(N) 알고리즘이 단계 수가 적다.
- 원소가 100개 보다 큰 모든 데이터 세트에서는 O(N) 알고리즘에 더 많은 단계가 필요하다.

데이터가 계속 증가하면 O(N)에 필요한 단계 수는 계속 증가하므로 O(1) 알고리즘에 실제로 몇 단계가 걸리든 O(N)이 전반적으로 O(1)보다 효율적이지 않다.

항상 100만 단계가 필요한 O(1) 알고리즘이라도 마찬가지다. 데이터가 증가할수록 O(N)이 O(1)보다 덜 효율적인 지점에 반드시 다다르게 되고, 이 지점 이후로 O(N)은 O(1) 보다 덜 효율적이다.

## 3.2.2 같은 알고리즘, 다른 시나리오

빅 오가 주어진 알고리즘의 최선과 최악의 시나리오를 설명하긴 하지만, 별도로 명시하지 않는 한 빅 오 표기법은 일반적으로 **최악의 시나리오**를 의미한다.

- 선형 검색이 최선의 시나리오에서 O(1)일 수 있음에도
- 대부분 O(N)이라 설명하는 이유이다.

최악의 시나리오에서 알고리즘이 얼마나 비효율적인지 정확히 알면 최악을 대비함과 동시에 알고리즘의 선택에 중요한 영향을 미친다.

# 3.3 세 번째 유형의 알고리즘

이진 검색을 빅 오 표기법 관점에서 어떻게 설명하는지 알아보자.

- 데이터가 커질수록 단계 수가 늘어나므로 O(1)이라 표기할 수 없다.
- 검색하고 있는 원소 수보다 단계 수가 훨씬 적으므로 O(N)에도 맞지 않는다.

이진 검색은 O(1)과 O(N) 사이 어디쯤엔가 있다. 빅 오는 이진 검색의 시간 복잡도를 다음과 같이 설명한다.

$O(logN)$

- "오 로그 N" 이라고 읽는다.
- 이런 유형의 알고리즘을 로그 시간(log time)의 시간 복잡도라고 한다.

O(logN)은 데이터가 두 배로 증가할 때마다 한 단계씩 늘어나는 알고리즘을 설명하는 빅 오의 방법이다. 이진 검색이 이 유형의 알고리즘이다. 데이터가 두 배로 증가해도 데이터를 절반으로 줄이는 한 단계만 추가되기 때문이다.

지금까지 배운 세 종류의 알고리즘을 가장 효율적인 순서대로 정렬하면 다음과 같다.

- O(1)
- O(logN)
- O(N)

![](https://images.velog.io/images/realryankim/post/29965e56-046a-4fd6-86ff-6d94c90e96fd/big-o-chart-tutorial-bazar-aymptotic-notations-1.png)

- O(logN)은 O(1)보다 덜 효율적이다.
- 하지만 O(logN)은 O(N)보다 훨씬 효율적이다.

# 3.4 로가리즘

로그는 무엇일까?

- 로그는 로가리즘의 줄임말이다.
- 로가리즘은 지수와 역의 관계다.

$2^3 = 2 \times 2 \times 2 = 8$이다. $log_28$은 $2^3$의 역이다.

즉, 2를 몇 번 곱해야 8을 얻을 수 있는지를 뜻한다. 2를 세 번 곱해야 8이므로 $log_28 = 3$이다.

밑이 2인 log8을 다른 방식으로 표현하면 다음과 같다.

- 1이 될 때까지 8을 2로 계속 나눌 때 얼마나 많은 2가 등장할까?
- 8 / 2 / 2 / 2 = 1
- 즉, 1이 나올 때까지 8을 2로 몇 번 나눠야 할까?
- 3이다.

따라서 $log_28 = 3$이다.

# 3.5 O(logN) 해석

컴퓨터 과학에서 $O(logN)$은 사실 $O(log_2N)$ 을 줄여 부르는 말이다. 편의를 위해 첨자 2를 생략한 것이다.

O(logN)은 데이터 원소 N개가 있을 때 알고리즘에 $log_2N$단계가 필요하다는 의미이다.

이진 검색이 정확히 이렇게 동작한다. 특정 항목을 찾을 때 정답 수에 도달할 때까지 배열의 셀을 계속해서 반으로 나누며 범위를 좁혀 나간다.

O(N) 알고리즘에는 데이터 원소 수만큼의 단계가 필요한 반면, O(logN) 알고리즘에는 데이터 원소가 두 배로 늘어날 때마다 딱 한 단계만 더 필요하다.

# 3.6 실제 예제

리스트 내 모든 항목을 출력하는 파이썬 코드이다.

```python
things = ['apples', 'baboons', 'cribs', 'dulcimers']

for thing in things:
  print("Here's a thing: $s", % thing)
```

이 알고리즘의 효율성을 빅 오 표기법으로 어떻게 표현할까?

- 이 코드는 리스트의 모든 항목을 출력하고 싶다는 문제를 해결한다.
- 이 문제를 푸는 데 사용한 알고리즘은 print 문이 포함된 for 루프이다.
- 이 예제에서는 알고리즘의 핵심부인 for 루프에서 4단계가 걸린다.
- 리스트는 원소 4개를 포함하며 한 번에 하나씩 원소를 출력한다.
- 이 과정은 상수가 아니다. 리스트에 원소가 10개이면 for 루프는 10단계가 걸린다.

따라서 for 루프에 원소 수만큼 단계가 걸리므로 이 알고리즘의 효율성은 O(N)이다.

다음은 주어진 수가 소수인지 알아보는 간단한 파이썬 기반 알고리즘이다.

```python
def is_prime(number):
  for i in range(2, number):
    if number % i == 0:
      return False
  return True
```

이 예제의 경우 앞선 예제들과 핵심 질문이 조금 다르다.

- 앞선 예제에서는 배열에 데이터 원소가 N개일 때 알고리즘에 몇 단계가 필요한지를 물었다.
- 여기서는 배열이 아니라 이 함수에 전달하는 number가 대상이다.
- 전달하는 number가 함수 루프 실행 횟수를 좌우한다.

이 예제에 맞는 핵심 질문은

- "number에 N을 전달할 때 알고리즘에 몇 단계가 필요할까?" 이다.
- 숫자 7을 전달하면 for 루프는 7단계를 실행한다.(실제로는 5단계)
- 숫자 101을 전달하면 for 루프는 101단계를 실행한다.

따라서 함수로 전달된 수에 비례해 단계 수가 증가하므로 전형적인 O(N) 유형의 알고리즘이다.

# 3.7 마무리

- 빅 오 표기법은 "데이터 원소가 N개일 때 알고리즘에 몇 단계가 필요할까?"에 대한 답이다.
- 빅 오의 본질이란 빅 오가 진정으로 의미하는 것, 즉 데이터가 늘어날 때 알고리즘의 성능이 어떻게 바뀌는지를 뜻한다.
- 빅 오 표기법은 어떤 알고리즘이라도 비교할 수 있는 일관된 시스템이다.
- 빅 오 표기법을 사용해 실제 쓰이는 시나리오를 분석해서 다양한 자료 구조와 알고리즘 중 사용자의 코드를 더 빠르게 하고 더 큰 부하도 처리할 수 있는 방법을 선택할 수 있다.