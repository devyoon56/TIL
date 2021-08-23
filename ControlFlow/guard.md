# guard 문 - 또다른 조건문

## guard 문을 사용하는 이유

1. if문의 불편함을 해소하고 코드 가독성을 높입니다.
2. 옵셔널 타입을 안전하게 벗길 수 있습니다.

## guard 문의 형태

```swift
guard 조건 else { return }
```

guard 문은 if 문과 같이 조건에 입력되는 표현식의 불리언 값에 따라 실행됩니다. guard 문 이후의 코드를 실행하기 위해서는 조건이 반드시 'true'이어야 합니다. 조건이 'false'라면 else 문이 실행되고 _조기 종료(early exit)_ 가능합니다.

guard의 조건이 'false' 일 때 *조기 종료*하기 위해 else 문 내부에 함수 또는 반복문을 종료시킬 코드가 필요합니다.

- 함수의 경우 return, throw
- 반복문의 경우 break, continue

## guard 문 예제

```swift
// 패스워드의 길이를 확인하는 함수
func checkPasswordCount(password: String) -> Bool {
    guard password.count >= 6 else {
        print("비밀번호가 6자리 미만입니다.")
        return false
    }

    print("비밀번호가 6자리 이상입니다.")
    return true
}

checkPasswordCount(password: "abcd1234")    // true
// 비밀번호가 6자리 이상입니다.

checkPasswordCount(password: "1a2b")    // false
// 비밀번호가 6자리 미만입니다.
```

```swift
// guard 문으로 옵셔널 언래핑
func greet(person: [String: String]) {
    // 딕셔너리[키]: 옵셔널 타입 반환
    guard let name = person["name"] else { return }

    print("안녕하세요 \(name)님!")

    guard let location = person["location"] else {
        print("근처 날씨가 좋았으면 좋겠습니다.")
        return
    }

    print("\(location) 날씨가 좋았으면 좋겠습니다.")
}

greet(person: ["name": "devyoon56"])
// 안녕하세요 devyoon56님!
// 근처 날씨가 좋았으면 좋겠습니다.

greet(person: ["name": "devyoon56", "location": "서울"])
// 안녕하세요 devyoon56님!
// 서울 날씨가 좋았으면 좋겠습니다.
```
