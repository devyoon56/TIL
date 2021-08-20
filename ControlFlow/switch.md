# switch 조건문

switch 조건문은 확인하고 싶은 변수 또는 상수의 경우의 수가 많아 if문에 모두 적기 힘들 때 if문보다 유용하게 사용할 수 있습니다.

## 1. Switch문의 형태

```swift
switch 확인하고싶은변수/상수 {
case 경우의수1:
//code
case 경우의수2:
//code
case 경우의수3:
//code
default: // 경우의수 1,2,3에 모두 해당되지 않는 경우
//code
}
```

switch문의 형태는 위와 같습니다.

switch 옆에 확인하고 싶은 변수 또는 상수명을 입력하고 각 case에 경우의 수를 명시합니다. case에 명시한 경우에 해당하면 case의 코드를 실행합니다.

## 2. 간단한 예제

```swift
var mySwiftSkill = 1

switch mySwiftSkill {
case 0:
	print("저는 스위프트 공부를 하지 않아요.")
case 1:
	print("스위프트를 처음 시작했어요.") // 출력
case 2:
	print("스위프트가 뭔지 알 것 같아요.")
case 3:
	print("스위프트에 익숙해요.")
case 4:
	print("스위프트는 훌륭해요.")
default:
	print("스위프트가 뭔가요?")
}
```

**mySwiftSkill** 변수를 선언하고 1을 할당하였습니다. 이후에 switch문을 사용하여 **mySwiftSkill** 변수 값에 맞는 case의 코드를 출력하였습니다.

이처럼 switch문을 사용하면 여러가지 선택 가능한 경우의 수에 따라 코드를 실행할 수 있습니다.

## 3. switch문을 사용할 때 주의할 점1

switch문을 사용할 때 주의할 점은 switch문은 **exhaustive(반드시 빠짐없이 철저)**해야 한다는 것입니다.

즉 확인하고자 하는 변수나 상수의 값이 case중 하나와는 반드시 일치해야 합니다. 모든 case를 나열할 수 없으면 default로 기본 case를 설정해야 합니다. default는 항상 마지막에 작성합니다.

```swift
let someChar: Character = "a"

switch someChar {
case "a":
	print("알파벳의 첫 번째 글자")
case "z":
	print("알파벳의 마지막 글자")
default:
	print("알파벳 a와 z 사이의 글자")
}
```

## 4. switch문을 사용할 때 주의할 점2

각 case의 코드는 반드시 실행할 코드를 포함해야 합니다. case의 코드를 작성하지 않으면 에러가 발생합니다.

```swift
let someChar: Character = "a"

switch someChar {
case "a":   // case에 코드가 없음
case "z":
	print("알파벳의 마지막 글자")
default:
	print("알파벳 a와 z 사이의 글자")
}
```

![](https://media.vlpt.us/images/cabbage56/post/6819e8ea-dc8c-4996-855a-6d8cd45edeb8/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-18%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.13.18.png)

case에서 아무 코드도 실행하고 싶지 않다면 **break**를 입력하면 됩니다.

```swift
let someChar: Character = "a"

switch someChar {
case "a":
	break
case "z":
	print("알파벳의 마지막 글자")
default:
	print("알파벳 a와 z 사이의 글자")
}
```

## 5. switch문의 패턴 매칭(pattern matching)

switch문에서 패턴 매칭이란 case를 범위로 구성하는 것을 말합니다.

```swift
var yourAge = 20

switch yourAge {
case 10...19:
	print("10대에요")
case 20...29:
	print("20대에요")   // 출력
case 30...39:
	print("저는 30대입니다")
default:
	break
}
```

yourAge 변수의 값이 어떤 범위에 포함되는지를 확인하고 범위에 맞는 코드를 실행합니다. 첫 번째 case부터 패턴 매칭을 통해 yourAge 변수의 값이 범위에 포함되는지 확인합니다.

yourAge 변수의 값은 **case 20...29**에 해당하므로 "20대에요"를 출력합니다. 이것은 패턴 매칭의 결과가 참이기 때문에 해당 case의 코드를 실행합니다.

그렇다면 패턴 매칭의 결과가 참인 것은 어떻게 확인할까요? 패턴 매칭은 패턴 매칭 연산자를 사용합니다. 패턴 매칭 연산자는 **~=**입니다.

패턴 매칭은 다음과 같이 적용됩니다. case의 범위와 yourAge 변수에 패턴 매칭 연산자를 적용하면 **true**를 반환합니다.

```swift
20...29 ~= yourAge // true
```

따라서 패턴 매칭의 결과, "20대에요"가 출력됩니다.

