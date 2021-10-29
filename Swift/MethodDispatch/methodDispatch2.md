# 메서드 디스패치의 세 가지 종류

메서드 디스패치의 세 가지 종류인 다이렉트 디스패치, 테이블 디스패치, 메세지 디스패치의 예시에 대해 알아봅니다.

## Direct Dispatch(정적 디스패치)

다이렉트 디스패치 방식은 값 타입에서 사용하는 방식입니다. 값 타입의 경우 상속 관계가 존재하지 않기 때문에 별도의 메서드 테이블을 생성할 필요가 없습니다. 따라서 가장 간단하고 가장 빠른 방식인 다이렉트 디스패치 방식을 사용합니다.

```swift
struct MyStruct {
    func method1() { print("Struct - Direct Method1") }
    func method2() { print("Struct - Direct Method2") }
}

let myStruct = MyStruct()
myStruct.method1()          // 컴파일 시점에 메서드 실행 주소 삽입
myStruct.method2()          // 컴파일 시점에 메서드 실행 주소 삽입
```

## Table Dispatch(동적 디스패치)

클래스는 배열 구조의 테이블에 클래스의 메서드 실행 주소(포인터)를 저장합니다. 클래스의 메서드를 실행하면 생성해놓은 배열 구조의 테이블에서 해당 메서드의 실행 주소를 참조하여 코드 영역의 메서드를 실행하는 방식입니다.

```swift
class FirstClass {
    func method1() { print("Class - Table method1") }
    func method2() { print("Class - Table method2") }
}

/**=========================================================
 FirstClass Virtual Table
 func method1() { print("Class - Table method1") } 실행 주소
 func method2() { print("Class - Table method2") } 실행 주소
============================================================**/

class SecondClass: FirstClass {
    override func method2() { print("Class - Table method2-2") }
    func method3() { print("Class - Table method3") }
}

/**============================================================
SecondClass Virtual Table
 func method1() { print("Class - Table method1") }    실행 주소
 func method2() { print("Class - Table method2-2") }  실행 주소
 func method3() { print("Class - Table method3") }    실행 주소
===============================================================**/

let first = FirstClass()
first.method1()             // 메서드 호출 시 클래스의 메서드 테이블 참조
first.method2()

let second = SecondClass()
second.method1()            // 메서드 호출 시 클래스의 메서드 테이블 참조
second.method2()
second.method3()
```

- 서브 클래스는 슈퍼 클래스와 다른 별도의 메서드 테이블을 생성한다.
- 슈퍼 클래스의 메서드 테이블을 그대로 가져오지만 상속한 메서드를 재정의하는 경우 해당 메서드의 실행 주소는 슈퍼 클래스와 다르다.
- 상속한 메서드의 실행 주소는 모두 슈퍼 클래스에서 가져오는 것이다.
- 상속한 메서드를 재정의한다면 메서드의 실행 주소는 슈퍼 클래스와 다르게 저장한다.

## Message Dispatch(메세지 디스패치)

메세지 디스패치는 Objective-C 에서 사용하던 방식입니다. 메세지 디스패치로 메서드를 동작하려면 **@objc dynamic** 키워드를 사용하여 메서드를 선언합니다.

```swift
class ParentClass {
    @objc dynamic func method1() { print("Class - Message method1") }
    @objc dynamic func method2() { print("Class - Message method2") }
}

/**================================================
 func method1() { print("Class - Message method1") }
 func method2() { print("Class - Message method2") }
===================================================**/

class ChildClass: ParentClass {
    @objc dynamic override func method2() { print("Class - Message method2-2") }
    @objc dynamic func method3() { print("Class - Message method3") }
}

/**================================================
 super class                                             // 슈퍼 클래스를 가리키는 포인터
 func method2() { print("Class - Message method2-2") }   // 재정의한 메서드는 별도의 주소를 가짐
 func method3() { print("Class - Message method3") }
===================================================**/

let parent = ParentClass()
parent.method1()
parent.method2()

let child = ChildClass()
child.method1()     // 슈퍼 클래스의 메서드 테이블을 찾아가서 해당 메서드 실행 주소 참조
child.method2()
child.method3()
```

- 테이블 디스패치와 다르게 서브 클래스는 슈퍼 클래스의 메서드 테이블을 모두 가져오지 않고 슈퍼 클래스의 메서드 테이블을 가리킨다.
- 서브 클래스가 상속한 메서드를 실행하는 경우 슈퍼 클래스의 메서드 테이블을 찾아가서 메서드를 실행하는 방식
- 서브 클래스가 상속한 메서드를 재정의하거나 새로운 메서드를 정의하는 경우 메서드 테이블에 새로운 메서드 실행 주소를 저장한다.
