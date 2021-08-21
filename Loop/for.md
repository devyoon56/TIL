# for-in 반복문

for-in 반복문은 수치 범위, 배열 또는 문자열에 있는 문자와 같은 '시퀀스'에 동작을 반복하기 위해 사용합니다.

## for-in 반복문의 형식

```swift
for 상수이름 in 시퀀스 {
    // code
}
```

시퀀스(수치 범위, 문자열, 컬렉션 타입)에서 item을 하나씩 뽑아서 for문 안에서 반복 실행합니다.

## for-in 반복문의 임시 상수에 대한 이해

```swift
for 임시상수 in 시퀀스 {
    // code
}
```

for와 in 사이의 임시상수는 변수가 아니라 상수라는 점을 주의해야 합니다.

## for-in 반복문의 범위(Scope)

for-in 문의 중괄호 내부에서 선언한 변수나 상수는 중괄호 밖에서 접근할 수 없습니다.
하지만 for-in 문의 중괄호 내부에서는 중괄호 외부의 변수나 상수에 접근할 수 있습니다.

```swift
var sum = 0

for i in 1...10 {
    sum += i
}

print(sum)  // 55
print(i)    // error
```

## for-in 반복문의 임시상수 생략

for-in 반복문에서 임시상수를 사용할 일이 없다면 언더바(\_)를 사용하면 됩니다.

```swift
for _ in 1...5 {
    print("hello"))
}
```

## 배열, 딕셔너리의 항목들에 동작을 반복

배열에 있는 항목들에 동작을 반복할 수 있습니다.

```swift
let swift = ["Swift", "Programming", "Language"]

for str in swift {
    print(str)
}
```

딕셔너리의 키-값(key-value) 쌍에 접근하기 위해 딕셔너리에 동작을 반복할 수 있습니다.

```swift
let numberOfLegs = ["human": 2, "dog": 4, "spider": 8]

for (name, legCount) in numberOfLegs {
    print("\(name)은 \(legCount)개의 다리를 갖고 있습니다.")
}
```

## for-in 반복문과 자주 사용하는 함수

- **reversed()**

```swift
for number in (1...5).reversed() {
    print(number)
}

// 5
// 4
// 3
// 2
// 1
```

- **stride(from:to:by)** 또는 **stride(from:through:by)**

```swift
for number in stride(from: 1, to: 15, by:2) {     // 마지막 숫자는 포함하지 않음
    print(number)
}
// 1, 3, 5, ..., 13

for number in stride(from: 1, through: 15, by:2) {     //마지막 숫자도 포함
    print(number)
}
// 1, 3, 5, ..., 13, 15
```
