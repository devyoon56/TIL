# WEB2 - JavaScript

# HTML과 JS의 만남: script 태그

**script 태그**

- 웹브라우저에게 HTML 코드로 자바스크립트가 시작된다고 알리는 태그
- 웹브라우저는 script 태그 내부를 자바스크립트로 해석

script 태그를 사용하는 html 예제 코드는 다음과 같다.

```html
<body>
  <h1>JavaScript</h1>
  <script>
    document.write("hello world");
  </script>
</body>
```

웹브라우저에서 결과를 확인하면 화면에 hello world가 출력된다.

# HTML과 JS의 만남: 이벤트

이벤트는 사용자와 상호작용하기 위한 핵심적인 역할을 한다.

```html
<body>
  <input type="button" value="hi" onclick="alert('hi')">
</body>
```

- onclick 속성의 값으로는 반드시 자바스크립트 코드를 사용해야 한다.
- 웹브라우저는 onclick 속성을 만나면 onclick 속성의 값을 기억한다.
- 사용자가 onclick 속성을 갖고 있는 태그를 클릭했을 때 웹브라우저가 기억하고 있던 자바스크립트 코드를 동작시킨다.

이와 같이 웹브라우저에서 일어나는 일들을 **이벤트**라고 한다. 웹브라우저에서 일어날 수 있는 이벤트와 이에 대응하는 속성은 다양한데, 이것들은 사용자들에게 유용할 만한 이벤트와 속성들이다.

대표적으로 아래와 같은 이벤트와 속성들이 있다.

- 클릭: onclick 속성
- 내용이 변경되었을 때: onchange 속성
- 키를 눌렀을 때: onkeydown 속성
- ...

```html
<body>
  <input type="button" value="hi" onclick="alert('hi')">
  <input type="text" onchange="alert('changed')">
  <input type="text" onkeydown="alert('key down')">
</body>
```

이런 이벤트와 이벤트에 대응하는 속성들을 사용하면 사용자와 상호작용하는 코드를 작성할 수 있다.

# HTML과 JS의 만남: 콘솔

어떤 코드를 가볍게 실행해야 하는 상황에서 콘솔을 사용할 수 있다.

- 크롬 기준: 웹브라우저 -> 개발자 도구 -> 콘솔
- 콘솔에서 자바스크립트 코드를 바로 실행할 수 있다.
- 별도의 파일을 생성하지 않아도 되어 간편하다.
- 어떤 웹페이지에서 콘솔을 사용하면 해당 웹페이지를 대상으로 콘솔을 사용하게 되어, 콘솔에서 해당 웹페이지를 대상으로 자바스크립트를 활용해 원하는 작업을 할 수 있다.

# 데이터 타입: 문자열과 숫자

자바스크립트의 값은 타입을 갖는다. 숫자 값은 숫자 타입을, 문자열 값은 문자열 타입을 갖는다.

```js
1        // 숫자 타입
'string' // 문자열 타입
"hi"     // 문자열 타입
```

# 변수와 대입 연산자

변수는 '바뀔 수 없는 어떤 값'이라고 할 수 있다. 변수에는 대입 연산자(=)를 사용해서 값을 대입할 수 있다.

```js
x = 1;
y = 2;
x + y;  // 3

x = 100;
x + y;  // 102
```

**var** 키워드를 사용해서 변수를 선언하면 된다.

```js
var name = 'egoing';
```

# 제어할 태그 선택하기

```html
<body>
  <input type="button" value="night">
  <input type="button" value="day">
</body>
```

button 타입의 input 태그를 클릭했을 때 body 태그의 style 속성을 동적으로, 프로그래밍적으로, 상호작용에 의해 변경하려고 한다. 먼저 자바스크립트 코드로 body 태그를 선택해야 한다.

```js
document.querySelector('body')
```

body 태그를 선택했으니 다음 단계로 body 태그의 style 속성을 변경해야 한다.

```js
document.querySelector('body').style
```

style 속성에 백그라운드 컬러를 변경하는 코드를 추가한다.

```js
document.querySelector('body').style.backgroundColor = 'black';
```

style 속성에 컬러를 변경하는 코드를 추가한다.

```js
document.querySelector('body').style.backgroundColor = 'black';
document.querySelector('body').style.color = 'white';
```

이 자바스크립트 코드를 value 속성 값이 "night"인 input 태그의 onclick 속성 값에 넣는다.

```html
<input type="button" value="night" onclick="
document.querySelector('body').style.backgroundColor = 'black';
document.querySelector('body').style.color = 'white';
">
```

이제 이 input 태그를 클릭하면 onclick 속성 값인 자바스크립트 코드에 따라 body 태그의 style 속성이 변경된다. (야간 모드)

이와 마찬가지로 아래의 자바스크립트 코드를 value 속성 값이 "day"인 input 태그의 onclick 속성 값에 넣는다.

```html
<input type="button" value="day" onclick="
document.querySelector('body').style.backgroundColor = 'white';
document.querySelector('body').style.color = 'black';
">
```

이제 이 input 태그를 클릭하면 onclick 속성 값인 자바스크립트 코드에 따라 body 태그의 style 속성이 변경된다. (주간 모드)

# 비교 연산자와 불리언

