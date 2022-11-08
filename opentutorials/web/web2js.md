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

```js
1 === 1  // true
1 === 2  // false

1 < 2    // true
1 < 1    // false
```

**불리언**

- true, false라는 두 개의 데이터로만 이루어진 데이터 타입

**비교 연산자 ===**

- 이항 연산자
- 좌항, 우항 값을 비교해서 같으면 true 반환, 다르면 false 반환

**비교 연산자 <**

- 이항 연산자
- 좌항, 우항 값을 비교해서 우항이 크면 true 반환, 우항이 작으면 false 반환

# 조건문

```js
document.write("1<br>");
if (true) {
  document.write("2<br>");
} else {
  document.write("3<br>");
}
document.write("4<br>");
```

브라우저 출력 결과: 1, 2, 4

```js
document.write("1<br>");
if (false) {
  document.write("2<br>");
} else {
  document.write("3<br>");
}
document.write("4<br>");
```

브라우저 출력 결과: 1, 3, 4

조건문은 if문의 괄호 안의 불리언 값에 따라 실행되는 코드를 바꾼다.

- 괄호 안에 true가 오면 if문의 코드 실행.
- 괄호 안에 false가 오면 else문의 코드 실행.

# 조건문의 활용

조건문을 활용해서 기존에 있던 두 개의 input 태그의 기능을 하나의 input 태그로 합칠 수 있다.

기존 두 개의 input 태그는 다음과 같다.

- 'night' 버튼을 클릭하면 야간 모드가 되고
- 'day' 버튼을 클릭하면 주간 모드가 된다.

```html
<input type="button" value="night" onclick="
  document.querySelector('body').style.backgroundColor = 'black';
  document.querySelector('body').style.color = 'white';
">
<input type="button" value="day" onclick="
  document.querySelector('body').style.backgroundColor = 'white';
  document.querySelector('body').style.color = 'black';
">
```

두 개의 input 태그를 다음과 같이 하나의 input 태그로 합친다.

```html
<input
  id="night_day"
  type="button"
  value="night"
  onclick="
    if (document.querySelector('#night_day').value === 'night') {
      document.querySelector('body').style.backgroundColor = 'black';
      document.querySelector('body').style.color = 'white';
      document.querySelector('#night_day').value = 'day';
    } else {
      document.querySelector('body').style.backgroundColor = 'white';
      document.querySelector('body').style.color = 'black';
      document.querySelector('#night_day').value = 'night';
    }
  "
/>
```

- 자바스크립트 코드로 요소를 제어하기 위해 input 태그의 id 속성 값을 "night_day"로 설정하였다.
- 주간 모드를 디폴트로 설정하고, value 속성 값을 초기에 "night"로 설정하여 야간 모드로 변경할 수 있게 하였다.
- if문 코드는 야간 모드로 변경하는 코드이다.
- else문 코드는 주간 모드로 변경하는 코드이다.
- 주야간 모드를 토글할 수 있도록 if문과 else문에서 value 값을 각각 'day'와 'night'로 설정한다.
  - 야간 모드 변경 시, value 값이 'day'가 되어 다시 주간 모드로 변경할 수 있게
  - 주간 모드 변경 시, value 값이 'night'이 되어 다시 야간 모드로 변경할 수 있게

# 리팩토링 중복의 제거

리팩토링은 비효율적인 코드를 효율적으로 개선하는 과정, 즉 코드의 가독성을 높이고 유지보수하기 편하게 만들고 중복 코드를 제거하는 과정이다.

이전의 코드

```html
<input
  id="night_day"
  type="button"
  value="night"
  onclick="
    if (document.querySelector('#night_day').value === 'night') {
      document.querySelector('body').style.backgroundColor = 'black';
      document.querySelector('body').style.color = 'white';
      document.querySelector('#night_day').value = 'day';
    } else {
      document.querySelector('body').style.backgroundColor = 'white';
      document.querySelector('body').style.color = 'black';
      document.querySelector('#night_day').value = 'night';
    }
  "
/>
```

이 코드를 리팩토링하면 아래 코드처럼 작성할 수 있다.

```html
<input
  type="button"
  value="night"
  onclick="
    var target = document.querySelector('body');
    if (this.value === 'night') {
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      this.value = 'day';
    } else {
      target.style.backgroundColor = 'white';
      target.style.color = 'black';
      this.value = 'night';
    }
  "
/>
```

- document.querySelector('body')가 중복되므로 중복을 제거하기 위해 target이라는 변수에 저장하고 변수를 사용하여 body 태그의 스타일을 변경한다.
- **this**: onclick과 같은 이벤트 안에서 실행되는 코드에서 자신이 속한 태그를 가리키도록 약속되어 있는 키워드이다. 여기서 this는 onclick 이벤트가 속한 태그인 input 태그를 가리킨다.
- document.querySelector('#night_day')를 this로 변경한다.
- 그리고 이제 id 속성은 필요하지 않으므로 id 속성을 삭제한다.

# 배열

프로그래밍을 하다 보면 굉장히 많은 데이터를 다루게 되는데, 그 데이터들은 제각각 성격이 모두 다르다.

소프트웨어가 복잡해질수록 다뤄야 할 데이터는 많아지고, 그 많은 데이터를 그냥 둘 수 없기 때문에, 그 데이터들 중에 서로 연관된 데이터를 잘 정리정돈해서 담아 두는 일종의 수납상자를 사용하게 된다. 이것을 배열array이라고 생각하면 된다.

```js
var coworkers = ["egoing", "leezche"];

document.write(coworkers[0]);  // egoing
document.write(coworkers[1]);  // leezche

document.write(coworkers.length);  // 2

coworkers.push("duru");
coworkers.push("taeho");
document.write(coworkers.length);  // 4
```

- coworkers라는 변수에 배열이라는 데이터 타입을 담는다.
- 대괄호를 사용해서 배열을 만들고, 대괄호와 인덱스를 사용해서 배열의 값을 읽는다.
- 배열의 length 프로퍼티를 사용해 배열의 크기를 얻을 수 있다.
- 배열의 push() 메서드를 사용해 배열에 데이터를 추가할 수 있다.

# 반복문

```js
var i = 0;
while (i < 3) {
  document.write('<li>2</li>');
  document.write('<li>3</li>');
  i = i + 1;
}
```

- while 반복문은 조건문처럼 실행할 코드를 제어한다.
- while 반복문은 괄호 안에 값이 true인 동안 반복 실행되고 괄호 안에 값이 false이면 종료된다.
- i의 값이 3보다 작으면 while 반복문의 코드는 계속 실행된다.
- i의 값이 0이므로 무한루프를 방지하기 위해 i의 값을 1씩 증가시킨다.
- 따라서 while 반복문은 총 3번 실행된다.

# 배열과 반복문

```js
var coworkers = ["egoing", "leezche", "duru", "taeho"];
var i = 0;

while (i < coworkers.length) {
  document.write('<li>' + coworkers[i] + '</li>');
  i = i + 1;
}
```

- coworkers 배열의 크기만큼 while 반복문을 반복 실행한다.
- coworkers 배열의 크기만큼 반복하는 것은 coworkers 배열에 원소를 추가하거나 삭제해도 while 반복문이 이에 맞춰 반복한다는 것을 의미한다.
- 따라서 coworkers 배열에 따라 유연하게 while 반복문이 실행된다.

# 배열과 반복문의 활용

이전 코드

```html
<input
  id="night_day"
  type="button"
  value="night"
  onclick="
    var target = document.querySelector('body');
    if (this.value === 'night') {
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      this.value = 'day';
    } else {
      target.style.backgroundColor = 'white';
      target.style.color = 'black';
      this.value = 'night';
    }
  "
/>
```

배열과 반복문을 활용해서 주야간 모드에서 눈에 잘 보이는 링크 색깔로 변경하는 코드를 작성한다.

야간 모드에서의 링크 색깔로 변경하는 코드

```js
var alist = document.querySelectorAll('a');
var i = 0;

while (i < alist.length) {
  alist[i].style.color = 'powderblue';
  i = i + 1;
}
```

- 모든 a 요소를 제어하기 위해 document.querySelectorAll 메서드를 사용한다.
  - 이 메서드는 정확히 배열을 반환하는 것은 아니다.
  - 노드 리스트를 반환하지만, 일단 배열이라고 생각하자.
- alist는 모든 a 요소를 담는 배열이다.
- alist의 각 원소에 접근해서 style 속성의 color를 'powderblue' 색으로 변경한다.

주간 모드에서의 링크 색깔로 변경하는 코드

```js
var alist = document.querySelectorAll('a');
var i = 0;

while (i < alist.length) {
  alist[i].style.color = 'blue';
  i = i + 1;
}
```

- alist의 각 원소에 접근해서 style 속성의 color를 'blue' 색으로 변경한다.

최종 코드

```js
var target = document.querySelector('body');
if (this.value === 'night') {
  target.style.backgroundColor = 'black';
  target.style.color = 'white';
  this.value = 'day';

  // 추가된 코드
  var alist = document.querySelectorAll('a');
  var i = 0;

  while (i < alist.length) {
    alist[i].style.color = 'powderblue';
    i = i + 1;
  }
} else {
  target.style.backgroundColor = 'white';
  target.style.color = 'black';
  this.value = 'night';

  // 추가된 코드
  var alist = document.querySelectorAll('a');
  var i = 0;

  while (i < alist.length) {
    alist[i].style.color = 'blue';
    i = i + 1;
  }
}
```

# 함수

```js
function two() {
  document.write('<li>2-1</li>');
  document.write('<li>2-2</li>');
}

document.write('<li>1</li>');
two();
document.write('<li>3</li>');
two();
```

- function 키워드로 함수를 선언한다.
- function 옆에 함수명, 괄호, 중괄호를 작성한다. 그리고 중괄호 안에 함수 코드를 작성한다.
- 함수 이름과 괄호를 사용해서 함수를 호출한다.

# 함수: 매개변수와 인자

함수는 입력과 출력으로 이루어진다.

함수 입력 관련 개념

```js
function sum(left, right) {
  document.write(left + right + '<br>');
}

sum(2, 3);  // 브라우저 화면에 5 출력
sum(2, 4);  // 브라우저 화면에 6 출력
```

- 함수 선언 시 괄호 안에 작성한 변수를 **parameter(매개변수)** 라고 한다.
  - 매개변수는 인자를 받아 함수 안으로 매개해주는 변수이다.
  - sum 함수의 매개변수는 left, right이다.
- 함수 호출 시 전달하는 값을 **argument(인자)** 라고 한다.
  - sum 함수 호출 시 전달하는 값인 2와 3은 매개변수 left, right에 대입된다.
  - 2와 4도 마찬가지다.

# 함수: 리턴

표현식

```js
1 + 1    // 2에 대한 표현식
2 - 1    // 1에 대한 표현식
1 === 1  // true에 대한 표현식
```

함수는 입력과 출력으로 이루어진다.

함수 출력 관련 개념

```js
function sum(left, right) {
  return left + right;
}

document.write(sum(2, 3) + '<br>');
document.write('<div style="color: red;">' + sum(2, 3) + '</div>');
document.write('<div style="font-size: 32px;">' + sum(2, 3) + '</div>');
```

- 함수 코드에서 return 키워드를 사용해 값을 반환한다.
- 표현식을 사용하여 값을 반환할 수 있다.
- sum 함수는 매개변수 left, right를 더한 결과를 반환한다.

# 함수의 활용

이전 코드

```html
<input
  type="button"
  value="night"
  onclick="
    var target = document.querySelector('body');
    if (this.value === 'night') {
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      this.value = 'day';

      var alist = document.querySelectorAll('a');
      var i = 0;

      while (i < alist.length) {
        alist[i].style.color = 'powderblue';
        i = i + 1;
      }
    } else {
      target.style.backgroundColor = 'white';
      target.style.color = 'black';
      this.value = 'night';

      var alist = document.querySelectorAll('a');
      var i = 0;

      while (i < alist.length) {
        alist[i].style.color = 'blue';
        i = i + 1;
      }
    }
  "
/>
```

onclick 속성 값인 자바스크립트 코드를 함수에 넣는다. head 태그의 script 태그를 작성하고 script 태그 안에 함수를 넣는다.

```js
function nightDayHandler(self) {
  var target = document.querySelector('body');
  if (self.value === 'night') {
    target.style.backgroundColor = 'black';
    target.style.color = 'white';
    self.value = 'day';

    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = 'powderblue';
      i = i + 1;
    }
  } else {
    target.style.backgroundColor = 'white';
    target.style.color = 'black';
    self.value = 'night';

    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = 'blue';
      i = i + 1;
    }
  }
}
```

onclick 속성 값에서 함수를 호출한다.

```html
<input
  type="button"
  value="night"
  onclick="
    nightDayHandler(this);
  "
/>
```

- 이전에 사용하던 this를 더이상 nightDayHandler 함수에서 사용할 수 없다.
  - this가 input 태그를 가리키지 않고 전역객체를 가리킨다.
  - input 태그의 onclick 속성 값에서 사용하던 코드라면 this가 input 태그를 가리킨다.
  - 하지만 이 코드를 따로 함수에 넣었으므로 this는 더이상 input 태그를 가리키지 않고 전역객체를 가리키게 된다.
  - 이해 못해도 넘어가기.
- this가 input 태그를 가리키게 하기 위해
  - 함수의 매개변수로 self를 선언하고 함수 코드에서 this를 사용했던 부분을 self로 변경한다.
  - 함수를 호출할 때 인자로 this를 전달한다.

# 객체 예고

객체를 정리정돈 도구라고 생각할 수 있다. 객체를 서로 연관된 변수와 서로 연관된 함수를 같은 이름으로 잘 그룹핑해서 잘 정리정돈하기 위한 도구라고 볼 수 있다.

# 객체

```js
var coworkers = {
  "programmer": "egoing",
  "designer": "leezche"
};

document.write("programmer: " + coworkers.programmer + "<br>");
document.write("designer: " + coworkers.designer + "<br>");

coworkers.bookkeeper = "duru";
document.write("bookkeeper: " + coworkers.bookkeeper + "<br>");

coworkers["data scientist"] = "taeho";
document.write("data scientist: " + coworkers["data scientist"] + "<br>");
```

- 객체 리터럴 방식으로 객체를 생성하고 coworkers 변수에 담는다.
- .(점)이라는 접근 연산자(액세스 오퍼레이터)를 사용해 객체에 담은 데이터를 가져올 수 있다.
- 접근 연산자를 사용해 객체에 데이터를 담을 수 있다.
- 또한 데이터 이름에 띄어쓰기가 있는 경우 대괄호와 따옴표를 사용해 객체에 데이터를 담을 수 있다.

# 객체와 반복문

```js
var coworkers = {
  "programmer": "egoing",
  "designer": "leezche"
};
coworkers.bookkeeper = "duru";
coworkers["data scientist"] = "taeho";

for (var key in coworkers) {
  document.write(key + ': ' + coworkers[key] + '<br>');
}
```

- 객체에서 키(key)라는 것은 데이터에 도달할 수 있는 열쇠를 말한다.
- coworkers 객체에서 키는 "programmer", "designer", "bookkeeper", "data scientist"이다.
- for문은 coworkers 객체에 있는 키 값들 하나하나를 변수 key에 할당하고, 각 변수 key에 대해 중괄호 내부의 코드를 실행한다.
- coworkers 객체에 대괄호와 키를 사용해서 키에 해당하는 데이터를 가져올 수 있다.
  - coworkers["programmer"]는 "egoing" 데이터를 가져온다.

# 객체 프로퍼티와 메소드

```js
var coworkers = {
  "programmer": "egoing",
  "designer": "leezche"
};
coworkers.bookkeeper = "duru";
coworkers["data scientist"] = "taeho";

// showAll 메소드 추가
coworkers.showAll = function () {
  for (var key in this) {
    document.write(key + ': ' + this[key] + '<br>');
  }
};

// showAll 메소드 호출
coworkers.showAll();
```

- 객체에 소속된 변수를 프로퍼티라고 한다.
  - "programmer", "designer", "bookkeeper", "data scientist" 프로퍼티
- 객체에 소속된 변수의 값으로 함수를 지정할 수 있다.
- 객체에 소속된 변수가 함수이면 그 함수를 메소드라고 한다.
  - showAll 메소드
- **this**: 객체에 소속된 메소드에서 객체를 가리키는 키워드

# 객체의 활용

이전 코드

```js
function nightDayHandler(self) {
  var target = document.querySelector('body');
  if (self.value === 'night') {
    target.style.backgroundColor = 'black';
    target.style.color = 'white';
    self.value = 'day';

    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = 'powderblue';
      i = i + 1;
    }
  } else {
    target.style.backgroundColor = 'white';
    target.style.color = 'black';
    self.value = 'night';

    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = 'blue';
      i = i + 1;
    }
  }
}
```

객체를 활용해서 코드를 개선한다.

```js
var Body = {
  setColor: function (color) {
    document.querySelector('body').style.color = color;
  },
  setBackgroundColor: function (color) {
    document.querySelector('body').style.backgroundColor = color;
  }
};
```

- Body 객체를 생성하고, body 요소의 폰트 색을 변경하는 setColor 메서드, 배경 색을 변경하는 setBackgroundColor 메서드를 추가한다.
- 객체의 프로퍼티나 메소드가 여러개라면 ,(콤마)로 구분한다.

```js
var Links = {
  setColor: function (color) {
    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = color;
      i = i + 1;
    }
  }
};
```

- Links 객체를 생성하고, 모든 a 요소의 폰트 색을 변경하는 setColor 메서드를 추가한다.

```js
function nightDayHandler(self) {
  if (self.value === 'night') {
    Body.setBackgroundColor('black');
    Body.setColor('white');
    self.value = 'day';

    Links.setColor('powderblue');
  } else {
    Body.setBackgroundColor('white');
    Body.setColor('black');
    self.value = 'night';

    Links.setColor('blue');
  }
}
```

- Body 객체의 setColor, setBackgroundColor 메소드로 body 요소의 폰트 색과 배경 색을 설정한다.
- Links 객체의 setColor 메소드로 모든 a 요소의 폰트 색을 설정한다.

```html
<input
  type="button"
  value="night"
  onclick="
    nightDayHandler(this);
  "
/>
```

# 파일로 쪼개서 정리정돈하기

서로 연관된 코드들을 파일로 묶어서 그룹핑할 수 있다.

새로운 자바스크립트 파일을 생성하고 공통되는 코드를 넣는다.

```js
var Body = {
  setColor: function (color) {
    document.querySelector('body').style.color = color;
  },
  setBackgroundColor: function (color) {
    document.querySelector('body').style.backgroundColor = color;
  }
};

var Links = {
  setColor: function (color) {
    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = color;
      i = i + 1;
    }
  }
};

function nightDayHandler(self) {
  if (self.value === 'night') {
    Body.setBackgroundColor('black');
    Body.setColor('white');
    self.value = 'day';

    Links.setColor('powderblue');
  } else {
    Body.setBackgroundColor('white');
    Body.setColor('black');
    self.value = 'night';

    Links.setColor('blue');
  }
};
```

이 자바스크립트 파일을 html 파일에서 사용할 수 있도록 script 태그의 src 속성에 자바스크립트 파일 경로를 값으로 넣는다.

```html
<head>
  <script src="ex.js"></script>
</head>
```

자바스크립트 파일을 사용하면 좋은 점

- 자바스크립트 파일을 수정하면 해당 파일을 사용하는 모든 웹페이지에 변경 사항이 적용된다.
  - 유지보수가 매우 편리해진다.
- 서로 다른 웹페이지에서 같은 자바스크립트 파일을 사용한다면 이 웹페이지가 같은 로직을 따른다는 것을 알 수 있다.
  - 가독성이 좋아지고 명확해진다.
- 코드의 의미를 파일 이름을 통해 알 수 있다.
- 한번 웹브라우저에 다운로드된 파일은 보통 컴퓨터에 저장된다. 그리고 한번 저장된 파일은 웹브라우저가 읽어서 네트워크를 통하지 않게 한다.
  - 네트워크 트래픽을 절감할 수 있다.
  - 웹페이지를 훨씬 더 빠르게 화면에 표시할 수 있다.
- 라이브러리를 프로젝트에 가져오는 데 중요한 역할을 한다.

# 라이브러리와 프레임워크

라이브러리

- 만들고자하는 프로그램에 필요한 부품이 되는 소프트웨어를 잘 정리정돈해놓은, 재사용하기 쉽도록 되어 있는 소프트웨어
- 라이브러리의 경우, 만들어진 소프트웨어를 끌어와서 사용하는 느낌.

프레임워크

- 만들고자 하는 것이 무엇이냐에 따라 그것을 만들려고 할 때 언제나 필요한 공통적인 것이 있고,
- 만들고자 하는 것에 대한 기획 의도에 따라서 달라지는 부분이 있다.
- 그 중에서 공통적인 부분은 프레임워크라는 것이 만들어놓고
- 만들고자 하는 것의 기능에 따라, 또는 개성에 따라 달라지는 부분만 수정하여
- 만들고자 하는 것을 처음부터 끝까지 모두 만들지 않도록 해주는 반제품과 같은 것을 프레임워크라고 할 수 있다.
- 프레임워크의 경우, 우리가 프레임워크 안에 들어가서 작업하는 느낌.

결국 라이브러리와 프레임워크는 협력하는 모델이다.

## jQuery 라이브러리

jQuery 라이브러리를 다운로드 받아 사용할 수도 있고, CDN을 통해 사용할 수도 있다.

구글 CDN을 사용하는 경우, script src를 사용해 jQuery를 사용하는 방법.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
```

이전 코드

```js
var Links = {
  setColor: function (color) {
    var alist = document.querySelectorAll('a');
    var i = 0;

    while (i < alist.length) {
      alist[i].style.color = color;
      i = i + 1;
    }
  }
};
```

jQuery 코드

```js
var Links = {
  setColor: function (color) {
    $('a').css('color', color);
  }
};
```

- $('a'): 웹페이지의 모든 a 태그를 jQuery로 제어하겠다.
- css 메소드를 사용해 모든 a 태그의 color 속성을 변경한다.

# UI vs. API

UI: User Interface

API: Application Programming Interface

```html
<input type="button" value="Click me" onclick="alert('Hello world')">
```

- 사용자는 버튼과 같은 조작 장치를 이용해서 웹 앱을 사용한다.
- 사용자가 시스템을 제어하기 위해 사용하는 조작 장치를 UI라고 부른다.
- 사용자가 input 태그를 클릭하면, 웹브라우저에 Hello world라는 경고창이 나온다.
- 웹브라우저를 만드는 사람들이 경고창 기능을 미리 만들어 두었다가 alert 함수를 실행하면 경고창을 띄워 주겠다는 걸 사용설명서를 통해 약속한 것이다.
- alert 함수는 경고창을 띄우는 조작 장치이다.
- 이 조작 장치는 사용자가 사용하지 않고, 웹 앱을 만드는 개발자들이 사용한다.
- 웹 앱을 만들기 위해 프로그래밍할 때 사용하는, 이러한 조작 장치들을 API라고 부른다.
- 이것은 자바스크립트에만 국한되지 않고, 모든 프로그래밍 언어에 공통적으로 적용된다.