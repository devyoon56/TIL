# 4장. 빅 오로 코드 속도 올리기

빅 오를 사용하면 내가 만든 알고리즘(내가 작성한 코드)와 이미 존재하는 범용 알고리즘을 비교할 수 있다.

내가 만든 알고리즘이 느린 알고리즘이라면 더 빠른 빅 오 카테고리에 들어갈 수 있게 최적화하는 방법을 찾아볼 수 있다.

# 4.1 버블 정렬

정렬 알고리즘은 다음의 문제를 해결하는 알고리즘이다.

> 정렬되지 않은 배열이 주어졌을 때, 어떻게 오름차순으로 정렬할 수 있을까?

기본적인 정렬 알고리즘으로 버블 정렬(bubble sort)은 다음 단계를 따른다. (배열 예제: [2, 1, 3, 5])

1. 배열 내에서 연속된 두 항목을 가리킨다.(처음에는 배열의 첫 번째 원소부터 시작해서 처음 두 항목을 가리킨다.) 첫 번째 항목과 두 번째 항목을 비교한다. 배열의 첫 번째 원소 2와 두 번째 원소 1을 비교한다.

2. 두 항목의 순서가 오름차순이 아니면(왼쪽 값이 오른쪽 값보다 크면) 두 항목을 교환(swap)한다. 배열의 첫 번째 원소 2와 두 번째 원소 1을 교환한다. 두 항목의 순서가 오름차순이면 아무것도 하지 않는다. (현재 배열: [1, 2, 3, 5])

3. 포인터를 오른쪽으로 한 셀씩 옮긴다. 배열의 두 번째 원소와 세 번째 원소를 가리킨다.

4. 배열의 끝까지 또는 이미 정렬된 값까지 1단계부터 3단계를 반복한다. 배열의 첫 패스스루(pass-through)가 끝났다. 즉 배열 끝까지 값을 하나하나 가리키며 배열을 통과하였다.

5. 이제 두 포인터를 다시 배열의 처음 두 값으로 옮겨 1단계부터 4단계를 다시 실행하여 새로운 패스스루를 실행한다. 교환이 일어나지 않을 때까지 패스스루를 반복한다. 교환할 항목이 없다는 것은 배열이 정렬됐고 배열을 오름차순으로 정렬했다는 의미이다.

# 4.2 버블 정렬 실제로 해보기

[4, 2, 7, 1, 3]이라는 배열을 정렬하고 싶다고 가정한다. 배열을 올바르게 오름차순으로 정렬하고 싶다.

첫 번째 패스스루

1. 먼저 4와 2를 비교한다.

2. 순서가 맞지 않으므로 둘을 교환한다. 결과: [2, 4, 7, 1, 3]

3. 다음으로 4와 7을 비교한다. 순서가 올바르다. 교환할 필요가 없다.

4. 7과 1을 비교한다.

5. 순서가 맞지 않으므로 둘을 교환한다. 결과: [2, 4, 1, 7, 3]

6. 7과 3을 비교한다.

7. 순서가 맞지 않으므로 둘을 교환한다. 결과: [2, 4, 1, 3, 7]

7은 이제 배열 내에서 확실히 올바른 위치에 있다. 적절한 위치에 도달할 때까지 7을 계속 오른쪽으로 옮겼기 때문이다.

이 알고리즘을 버블 정렬이라고 부르는 까닭은 각 패스스루마다 정렬되지 않은 값 중 가장 큰 값, "버블"이 올바른 위치로 이동하기 때문이다.

첫 번째 패스스루에서 교환을 적어도 한 번 수행했으니 다음 패스스루도 수행해야 한다.

두 번째 패스스루

8. 2와 4를 비교한다. 순서가 올바르다. 교환하지 않는다.

9. 4와 1을 비교한다.

10. 순서가 맞지 않으므로 둘을 교환한다. 결과: [2, 1, 4, 3, 7]

11. 4와 3을 비교한다.

12. 순서가 맞지 않으므로 둘을 교환한다. 결과: [2, 1, 3, 4, 7]

7은 이미 올바른 위치라는 것을 알고 있으니 4와 7은 비교할 필요가 없다. 또한 4 역시 올바른 위치에 이동하였다. 결과: [2, 1, 3, 4, 7]. 두 번째 패스스루가 끝났다.

두 번째 패스스루에서 교환을 적어도 한 번 수행했으니 다음 패스스루도 수행해야 한다.

세 번째 패스스루

13. 2와 1을 비교한다.

14. 순서가 맞지 않으므로 둘을 교환한다. 결과: [1, 2, 3, 4, 7]

15. 2와 3을 비교한다. 순서가 올바르다. 교환하지 않는다.

3이 이제 올바른 위치에 이동하였다. 결과: [1, 2, 3, 4, 7]. 세 번째 패스스루가 끝났다.

세 번째 패스스루에서 교환을 적어도 한 번 수행했으니 다음 패스스루도 수행해야 한다.

네 번째 패스스루

16. 1과 2를 비교한다. 순서가 올바르다. 교환하지 않는다.

나머지 값은 모두 이미 올바르게 정렬됐으니 네 번째 패스스루를 종료한다.

어떤 교환도 하지 않은 패스스루였으므로 이제 이 배열은 완전히 정렬됐다. 결과: [1, 2, 3, 4, 7]

## 4.2.1 버블 정렬 구현

파이썬으로 구현한 버블 정렬 코드

```python
def bubble_sort(list):
  unsorted_until_index = len(list) - 1
  sorted = False

  while not sorted:
    sorted = True
    for i in range(unsorted_until_index):
      if list[i] > list[i + 1]:
        list[i], list[i + 1] = list[i + 1], list[i]
        sorted = False
    unsorted_until_index -= 1

  return list
```

### 코드와 코드 설명

```python
unsorted_until_index = len(list) - 1
```

- unsorted_untile_index 변수는 아직 정렬되지 않은 배열의 가장 오른쪽 인덱스를 기록한다.
- 알고리즘 첫 시작 시 전체 배열이 정렬되지 않은 상태이므로 배열의 마지막 인덱스로 변수를 초기화한다.

```python
sorted = False
```

- sorted 변수는 배열의 정렬 여부를 기록한다.
- 알고리즘 첫 시작 시 배열이 정렬되지 않은 상태이므로 False를 할당한다.

```python
while not sorted:
```

- 배열이 정렬될 때까지 계속 실행될 while 루프를 처리한다.
- 루프 한 번 실행이 배열의 한 패스스루에 해당한다.

```python
sorted = True
```

- 이어서 sorted에 True를 할당한다.
- 각 패스스루에서 교환이 일어나기 전까지 배열이 정렬되어 있다고 가정한다.
- 그리고 값을 교환하는 경우 sorted 변수를 다시 False로 바꾸는 방식이다.
- 이렇게 해야 어떤 교환도 일어나지 않고 패스스루를 통과할 때 sorted가 True로 남아 배열이 완전 정렬된 상태임을 알 수 있다.

```python
for i in range(unsorted_until_index):
```

- while 루프 내에서 for 루프를 시작한다.
- 루프 안에서는 배열 내 모든 값 쌍을 가리킨다.
- 변수 i를 포인터로 사용해 배열의 첫 인덱스부터 아직 정렬되지 않은 인덱스까지 수행한다.

```python
if list[i] > list[i + 1]:
  list[i], list[i + 1] = list[i + 1], list[i]
  sorted = False
```

- for 루프 내에서 모든 인접 값 쌍을 비교하고 순서가 뒤바뀌어 있으면 교환한다.
- 또한, 교환하면 sorted를 False로 바꾼다.

```python
unsorted_until_index -= 1
```

- 각 패스스루가 끝나면 오른쪽으로 올려준 버블이 이제 올바른 위치에 있음을 알 수 있다.
- 즉, 기존에 가리키던 인덱스가 정렬된 상태가 되었으니 unsorted_until_index를 1 감소시킨다.

```python
return list
```

- sorted가 True가 되면, 즉 배열이 완전 정렬되면 while 루프를 종료한다.
- 그리고 정렬된 배열을 반환한다.

# 4.3 버블 정렬의 효율성

버블 정렬 알고리즘은 두 가지 중요한 단계를 포함한다.

- 비교: 어느 쪽이 더 큰지 두 수를 비교한다.
- 교환: 정렬하기 위해 두 수를 교환한다.

## 버블 정렬의 비교

먼저, 4.2절에서 배열 [4, 2, 7, 1, 3]을 버블 정렬 알고리즘으로 정렬하는 과정에서 얼마나 많은 비교가 일어났을까?

예제의 배열은 원소가 5개다.

- 첫 번째 패스스루에서 두 수의 비교를 4번 해야 했다.
- 두 번째 패스스루에서 비교를 3번 해야 했다. (첫 번째 패스스루에서 버블이 올바르게 위치하므로)
- 세 번째 패스스루에서 비교를 2번 해야 했다.
- 네 번째 패스스루에서 비교를 1번 해야 했다.
- 따라서 비교의 총합은 10번이다.

모든 배열 크기에 적용되도록 표현하면 원소 N개에 대해서,

(N - 1) + (N - 2) + ... + 1 번의 비교를 수행한다.

## 버블 정렬의 교환

원소가 5개인 배열이 내림차순으로 정렬된 최악의 시나리오라면 비교할 때마다 교환을 해야 한다.

- 비교 10번
- 교환 10번
- 총 20단계 필요

원소가 10개인 배열이 내림차순으로 정렬된 최악의 시나리오라면 비교할 때마다 교환을 해야 한다.

- 비교 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 = 45번
- 교환 45번
- 총 90단계 필요

원소가 20개인 배열이 내림차순으로 정렬된 최악의 시나리오라면 비교할 때마다 교환을 해야 한다.

- 비교 19 + 18 + 17 + ... + 3 + 2 + 1 = 190번
- 교환 190번
- 총 380번

원소 수가 증가할 수록 단계 수가 기하급수적으로 늘어난다.

N이 증가할 때마다 단계 수가 얼마씩 늘어나는지 살펴보면 대략 $N^2$만큼 늘어나는 것을 알 수 있다.

값이 N개이므로 버블 정렬에는 $N^2$단계가 필요하고, 빅 오로 나타내면 버블 정렬의 효율성은

$$
O(N^2)
$$

이다.

$O(N^2)$은 데이터가 증가할 때 단계 수가 급격히 늘어나므로 비교적 비효율적인 알고리즘이다.

![](https://images.velog.io/images/realryankim/post/29965e56-046a-4fd6-86ff-6d94c90e96fd/big-o-chart-tutorial-bazar-aymptotic-notations-1.png)

단순히 대각선을 그리는 O(N)과 비교했을 때도 $O(N^2)$의 단계 수가 매우 급격히 증가한다.

$O(N^2)$을 이차 시간(quadratic time)이라고도 부른다.

# 4.4 이차 문제

느린 $O(N^2)$ 알고리즘을 $O(N)$ 알고리즘으로 대체할 수 있는 현실적인 예제

- 사용자가 제품에 대해 1부터 10사이로 매긴 평점을 분석하는 자바스크립트 애플리케이션
- 평점 배열에 중복 숫자가 들어 있는지 확인하는 함수 작성
- 예를 들어 배열 [1, 5, 3, 9, 1, 4]에는 숫자 1이 두 번 나오므로 true를 반환하여 중복 숫자가 있다고 알림

가장 먼저 떠오르는 방법 중 하나가 다음과 같이 중첩 루프를 사용하는 것이 아닐까.

```js
function hasDuplicateValue(array) {
  for (let i = 0; i < array.length; i++) {
    for (let j = 0; j < array.length; j++) {
      if (i !== j && array[i] === array[j]) {
        return true;
      }
    }
  }
  return false;
}
```

위 코드는 잘 동작하긴 하지만 과연 효율적일까? 이 함수를 빅 오로 어떻게 표현할까?

빅 오를 위 코드에 적용하려면 이렇게 물어야 한다.

- hasDuplcateValue 함수에 값 N개를 포함하는 배열이 주어졌을 때, 최악의 시나리오에서 알고리즘에 얼마나 많은 단계가 필요한가?

이 질문에 답하려면 먼저 어떤 단계가 필요한지, 그리고 최악의 시나리오는 어떤 경우인지 분석해야 한다.

- 이 함수에는 비교가 있다. 반복해서 i와 j를 비교해서 중복 쌍인지를 확인한다.
- 최악의 시나리오는 배열이 중복 값을 포함하지 않는 경우다. 이 경우 코드는 false를 반환하기 전에 모든 루프를 수행하고 가능한 모든 조합을 비교해야 한다.

결론적으로 배열에 값 N개가 있을 때 함수는 $N^2$번 비교를 수행한다.

- 바깥 루프는 배열을 전부 살펴보기 위해 무조건 N번을 순회하고,
- 순회마다 안쪽 루프는 다시 N번을 순회한다.
- 따라서 N단계 * N단계 = $N^2$ 이므로 $O(N^2)$의 알고리즘이다.

루프 내에 다른 루프를 중첩하는 알고리즘이라면 대부분 $O(N^2)$이다.

- 중첩 루프는 $O(N^2)$ 알고리즘이라는 것에 주의해야 한다.

$O(N^2)$은 느린 알고리즘으로 간주된다. 느린 알고리즘을 마주하면 더 빠른 대안이 없을지 깊이 생각하는 것이 좋다.

# 4.5 선형 해결법

중첩 루프를 쓰지 않는 hasDuplicateValue 함수를 구현할 수 있다.

```js
function hasDuplicateValue(array) {
  let existingNumbers = [];
  for (let i = 0; i < array.length; i++) {
    if (existingNumbers[array[i]] === 1) {
      return true;
    } else {
      existingNumbers[array[i]] = 1;
    }
  }
  return false;
}
```

## 함수 코드 설명

1. existingNumbers라는 빈 배열을 생성한다.

2. 루프를 사용해 array의 각 숫자를 확인한다. 숫자가 나올 때마다 existingNumbers 배열에서 그 숫자에 해당하는 인덱스에 1을 넣는다.

예를 들어 배열 [3, 5, 8]이 있다면 3이 나오면 existingNumbers의 인덱스 3에 1을 넣는다.

```js
// existingNumbers
[undefined, undefined, undefined, 1]
```

인덱스 3에 1이 있으니 앞으로 주어진 array에 이미 3이 나왔었음을 알고 기억할 수 있다.

다음으로 array에 5가 나오면 existingNumbers의 인덱스 5에 1을 넣는다.

```js
// existingNumbers
[undefined, undefined, undefined, 1, undefined, 1]
```

그리고 8이 나오면 existingNumbers의 인덱스 8에 1을 넣는다.

```js
// existingNumbers
[undefined, undefined, undefined, 1, undefined, 1, undefined, undefined, 1]
```

본질적으로 existingNumbers의 인덱스를 사용해 지금까지 array에서 어떤 숫자들이 나왔었는지 기억한다.

3. 적절한 인덱스에 1을 저장하기 앞서 이 인덱스의 값이 이미 1인지 확인한다.

    - 1이면 이미 나왔던 숫자라는 의미이며 중복 값을 찾은 것이므로 true를 반환하고 함수를 도중에 중단.
    - true를 반환하지 않고 루프 끝까지 갔다면 중복 값이 없는 것이므로 false 반환.

## 빅 오 관점에서 새로운 알고리즘의 효율성

이 새로운 알고리즘의 효율성을 빅 오 관점에서 알아내려면 최악의 시나리오일 때 알고리즘에 필요한 단계 수를 알아내야 한다.

이 알고리즘에 포함된 단계 중 주요 유형은 각 숫자를 보고 existingNumbers에서 해당 인덱스의 값이 1인지 확인하는 것이다.

```js
if (existingNumbers[array[i]] === 1)
```

최악의 시나리오는 배열에 중복 값이 없을 때 발생한다. 이때 함수는 전체 루프를 모두 수행해야 한다.

- 새로운 알고리즘은 데이터 원소 N개가 있을 때 비교를 N번하는 것 같다.
- 단 하나의 루프에서 단지 배열에 있는 원소 수만큼 순회하기 때문이다.

이 알고리즘은 O(N)이다. O(N)은 $O(N^2)$보다 훨씬 빠르므로 두 번째 접근법을 사용하여 hasDuplicateValue를 크게 최적화하였다.

이 알고리즘의 단점

- 첫 번째 방식보다 메모리를 더 소비한다는 것.
- 아직은 신경 쓰지 말고 넘어가자.

# 4.6 마무리

- 빅 오 표기법을 이해하면 느린 코드를 식별하고 두 경쟁 알고리즘 중 더 빠른 알고리즘을 선택 가능하다.
- 빅 오 표기법에서 두 알고리즘의 속도가 같더라도 실제로는 어느 한쪽이 더 빠른 상황이 발생하는데, 5장에서 빅 오 표기법으로 유의미한 차이를 발견할 수 없는 알고리즘들의 효율성 평가 방법을 배운다.