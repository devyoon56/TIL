# 중첩 타입(Nested Type)의 개념

타입 내부에 타입을 선언하는 것을 중첩 타입이라고 합니다. 타입 내부에 얼마던지 타입을 선언할 수 있습니다.

## 중첩 타입의 예시

다음은 중첩 타입의 간단한 예시입니다.

```swift
class Aclass {
    struct Bstruct {
        enum Cenum {
            case aCase
            case bCase

            struct Dstruct {}
        }

        var name: Cenum
    }
}
```

이렇게 선언된 중첩 타입의 인스턴스는 다음과 같이 생성할 수 있습니다.

```swift
let aClass: Aclass = Aclass()

let bStruct: Aclass.Bstruct = Aclass.Bstruct(name: Cenum.aCase)

let cEnum: Aclass.Bstruct.Cenum = Aclass.Bstruct.Cenum.aCase

let dStruct: Aclass.Bstruct.Cenum.Dstruct = Aclass.Bstruct.Cenum.Dstruct()
```

## 중첩 타입의 사용 이유

1. 특정 타입 내부에서만 사용할 타입을 선언하는 경우가 있다.
2. 타입 간의 연관성을 명확하게 구분할 수 있고 타입 내부 구조를 디테일하게 설계할 수 있다.

   - 위 예시를 보면 Bstruct가 Aclass 내부에 선언되어 있다.
   - Bstruct가 Aclass와 연관이 있고 Aclass 없이 자체적으로 사용했을 때 무의미한 경우가 있다.
   - 따라서 Aclass 내부에서만 사용할 수 있도록 범위를 명확하게 하는 것이다.

타입 내부에 선언된 타입은 위와 같은 경우로 이해할 수 있습니다.
