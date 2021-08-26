# 집합 Set

Set은 스위프트의 컬렉션 중에 하나입니다. 세트는 수학의 집합과 비슷하다고 볼 수 있습니다.

그리고 세트는 딕셔너리처럼 순서가 없는 컬렉션입니다. 또 딕셔너리의 키와 비슷하게 세트의 요소는 _Hashable_ 해야 합니다.

## 1. 세트의 문법

- 배열과 동일하게 대괄호 []를 사용합니다.
- 따라서 배열과 구별하기 위해 타입을 명시해야 합니다.
- 수학의 집합과 비슷하므로 세트의 요소들은 중복되지 않습니다.

```swift
var array: [Int] = [1, 2, 2, 3, 3, 3]
var mySet: Set<Int> = [1, 2, 2, 3, 3, 3]

print(array)    // [1, 2, 2, 3, 3, 3]
print(mySet)    // [2, 1, 3]
```

## 2. 세트는 언제 그리고 왜 사용할까

이전에도 언급했듯이 세트의 요소는 **Hashable** 해야 합니다.(Hashable하다는 의미는 해시 함수의 입력값이 될 수 있다는 의미인데 이것은 Hashable 내용에서 다루겠습니다.) 세트의 요소는 Hashable 하므로 요소의 정렬 순서보다 요소의 검색 속도가 중요한 경우에 사용합니다. 세트는 내부적으로 값을 검색하는데 Hashing 알고리즘을 사용하므로 값의 검색 속도가 매우 빠릅니다.

Hashing 알고리즘은 특정값을 고정된 길이의 유일한 값으로 변환하는 기법으로 인덱싱과 암호화에서 자주 사용되는 개념입니다.

또한 세트는 요소가 유일하기 때문에 집합의 수학적인 개념(합집합 등의 개념)을 사용할 필요가 있을 때 사용합니다. 간편한 집합 연산을 내장하고 있기 때문에 집합 연산을 쉽게 계산할 수 있습니다.

## 3. 세트의 타입 표기

세트의 타입을 표기하는 두 가지 방법이 있습니다.

```swift
// 단축 표기
let mySet: Set = [1, 2, 3]

// 정식 표기
let mySet2: Set<Int> = [1, 2, 3]
```

## 4. 빈 세트 생성하기

```swift
let emptySet1: Set<Int> = []
let emptySet2 = Set<Int>()
```

## 5. 세트의 기본 기능

```swift
var mySet: Set<Int> = [1, 2, 2, 3, 3, 3]

mySet.count     // 3

mySet.isEmpty   // false

mySet.contains(2)   // true
mySet.contains(4)   // false

mySet.randomElement()   // 3
```

## 6. 세트 업데이트하기(삽입, 교체, 추가하기)

세트에는 서브스크립트와 관련된 문법이 없습니다. 세트에 요소를 추가하려면 update(with:)를 사용합니다.

또한 세트에는 딕셔너리와 같은 이유로 append 함수가 없습니다. 세트는 순서가 없는 컬렉션이기 때문입니다.

```swift
var mySet: Set<Int> = [1, 2, 2, 3, 3, 3]

mySet.update(with: 3)   // 3, 추가한 값이 이미 있다면 기존의 요소 반환
mySet.update(with: 7)   // nil, 새로운 요소가 추가되면 nil 반환
```

```swift
// 삭제하기
var apple: Set<String> = ["Mac", "iPhone", "AirPods", "AppleTV", "iPod"]

apple.remove("iPod")        // iPod, 삭제한 요소 반환
apple                       // ["Mac", "AppleTV", "AirPods", "iPhone"]

apple.remove("PowerMac")    // nil, 존재하지 않는 요소 삭제 시 nil 반환

apple.removeAll()           // 전체 요소 삭제
apple.removeAll(keepingCapacity: true)  // 컬렉션 메모리 공간 유지하면서 전체 요소 삭제
```

## 7. 세트의 활용

세트에는 집합의 수학 연산을 수행하는 다양한 함수가 내장되어 있습니다.

```swift
var a: Set = [1, 2, 3, 4, 5, 6, 7, 8, 9]
var b: Set = [1, 3, 5, 7, 9]        // 홀수
var c: Set = [2, 4, 6, 8, 10]       // 짝수
var d: Set = [1, 7, 5, 9, 3]        // 홀수

b.isSubset(of: a)   // true, 부분집합 여부 판단
b.isStrictSubset(of: a)     // true, 진부분집합 여부 판단

a.isSuperset(of: b) // true, 상위집합 여부 판단
a.isStrictSuperset(of: b)   // true, 진상위집합 여부 판단

d.isDisjoint(with: c)   // true, 서로소 여부 판단
```

```swift
var a: Set = [1, 2, 3, 4, 5, 6, 7, 8, 9]
var b: Set = [1, 3, 5, 7, 9]        // 홀수
var c: Set = [2, 4, 6, 8, 10]       // 짝수
var d: Set = [1, 7, 5, 9, 3]        // 홀수

// 합집합
var union = b.union(c)      // {4, 3, 9, 1, 2, 7, 5, 6, 8, 10}

// 교집합
var inter = b.intersection(a)   // {7, 5, 3, 1, 9}

// 차집합
var sub = a.subtracting(b)      // {2, 6, 8, 4}

// 대칭차집합
var symmetric = a.symmetricDifference(b)    // {2, 6, 8, 4}
```

```swift
// 반복문과의 결합
let iterationSet: Set = [3, 2, 4, 5]

// 세트는 순서가 없는 컬렉션이므로 실행할 때마다 결과가 다르다
for num in iterationSet {
    print(num)
}

// 3
// 5
// 2
// 4
```

세트를 정렬하면 순서가 있는 배열로 리턴합니다.

```swift
var intSet: Set = [5, 2, 4, 1, 6, 0]
var sortedSet = intSet.sorted()     // 세트 오름차순 정렬

print(sortedSet)
// [0, 1, 2, 4, 5, 6] 출력
```
