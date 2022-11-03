# WEB2 - CSS

## CSS가 등장하기 이전의 상황

HTML 등장 이후 웹페이지의 디자인을 바꾸고 싶어하는 수요가 증가하였다.

  - 폰트를 변경하고 싶어요
  - 글씨 색깔을 변경하고 싶어요
  - ...

HTML 태그를 사용하여 디자인을 변경하려는 시도가 있었다. 하지만 HTML 태그는 정보를 표현한다는 목적을 가지고 있다. 예를 들어 h1 태그는 제목을, a 태그는 링크라는 정보를 나타낸다.

그러나 디자인 요소를 표현하는 HTML 태그는 h1 태그, a 태그와는 다르게 어떠한 정보도 표현하지 않는다. 예를 들어 이 글씨의 폰트가 무엇이고 무슨 색깔을 갖는다는 디자인을 나타낼 뿐이다. 디자인은 중요하지만 디자인 자체가 정보라고 할 수 없다. 예를 들어 시각장애인들의 경우를 생각해 봤을 때, 볼 수 없는 것은 정보가 아니라고 생각할 수 있다.

HTML 태그를 사용하여 디자인을 변경하게 되면 정보를 표현하는 HTML 태그와 디자인을 표현하는 HTML 태그가 섞이면서 웹페이지가 정보로서 갖는 가치를 떨어뜨리는 문제점이 발생한다. 결국 HTML 태그를 사용하여 디자인을 변경하는 것이 아니라 디자인을 변경할 수 있는 새로운 기술을 고안하기 시작하였다.

## CSS의 등장

아래에 예제 코드가 있다. 이 코드에서 font 태그는 글씨 색을 빨간색으로 변경한다. 하지만 이 방법은 HTML의 목적성에서 벗어난다.

```html
<h1><a href="index.html"><font color="red">WEB</font></a></h1>
<ol>
  <li><a href="1.html"><font color="red">HTML</font></a></li>
  <li><a href="2.html"><font color="red">CSS</font></a></li>
  <li><a href="3.html"><font color="red">JavaScript</font></a></li>
</ol>
```

HTML은 정보를 표현한다는 목적이 있으므로 디자인 기능을 전담하는 CSS를 사용해 글씨 색을 변경해야 한다. 웹페이지에 CSS를 적용하는 방법 중 하나로 head 태그 내부에 style 태그를 사용하는 방법이 있다.

style 태그는 웹브라우저에게 태그 내부의 코드를 CSS로 해석하라는 의미를 전달하는 태그이다.

```html
<head>
  <style>
    /* 웹페이지의 모든 a 태그에 대해서 스타일을 적용하라는 의미 */
    a {
      color: red;
    }
  </style>
</head>
<body>
  <h1><a href="index.html">WEB</a></h1>
  <ol>
    <li><a href="1.html">HTML</a></li>
    <li><a href="2.html">CSS</a></li>
    <li><a href="3.html">JavaScript</a></li>
  </ol>
</body>
```

이와 같이 style 태그와 CSS 문법을 사용하면 웹페이지의 모든 a 태그에 대해서 스타일을 적용할 수 있다.

이렇게 CSS로 웹페이지를 디자인하면 HTML로 웹페이지를 디자인하는 것보다 훨씬 더 효율적이다. 이 점은 첫 번째 예제 코드를 보면 알 수 있는데 font 태그가 4번 등장하고 중복된다. 이것은 코드 유지보수를 어렵게 하고 가독성까지 떨어진다. 예제 코드에서는 font 태그가 4번 등장하지만 만약 1억번 등장한다면 어떨까?

정리하자면 **CSS의 등장 배경**은 다음과 같다.

1. HTML이 정보를 표현하는 것에 전념하도록 디자인 기능을 전담하기 위함
2. CSS로 웹페이지를 디자인하는 것이 HTML로 디자인하는 것보다 훨씬 더 효율적임

## CSS의 기본 문법

CSS를 적용하는 여러 방법이 있는데 두 가지 방법에 대해 알아보자.

1. style 태그를 사용하는 방법
2. HTML 태그에 style 속성을 사용하는 방법

첫 번째로 style 태그를 사용하는 방법은 다음과 같다. style 태그를 head 태그 내부에 넣고 style 태그 내부에 CSS 문법을 사용하는 것이다.

```html
<head>
  <style>
    a {
      color: red;
    }
  </style>
</head>
<body>
  <h1><a href="index.html">WEB</a></h1>
  <ol>
    <li><a href="1.html">HTML</a></li>
    <li><a href="2.html">CSS</a></li>
    <li><a href="3.html">JavaScript</a></li>
  </ol>
</body>
```

style 태그 내부의 CSS 코드는 다음과 같다.

```css
a {
  color: red;
}
```

이것은 모든 a 태그에 대해 글씨 색을 빨간색으로 변경하라는 CSS 문법에 따라 코드를 작성한 것이다. 이 문법은 스타일을 적용할 a 태그를 선택한다는 의미에서 **셀렉터(selector)** 라고 한다.

두 번째로 HTML 태그에 style 속성을 사용하는 방법은 다음과 같다. 아래 예제 코드와 같이 CSS 코드를 적용할 태그에 style 속성을 사용하는 것이다. 이 방법은 해당 태그에 스타일을 바로 적용하므로 셀렉터를 사용할 필요가 없다.

```html
<head>
  <style>
    a {
      color: black;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <h1><a href="index.html">WEB</a></h1>
  <ol>
    <li><a href="1.html">HTML</a></li>
    <li>
      <a href="2.html" style="color: red; text-decoration: underline;">CSS</a>
    </li>
    <li><a href="3.html">JavaScript</a></li>
  </ol>
</body>
```

```html
<a href="2.html" style="color: red; text-decoration: underline;">CSS</a>
```

두 번째 li 태그에 있는 a 태그의 style 속성의 값을 보면 CSS 문법에 따라 CSS 코드를 사용한 것을 확인할 수 있다.

style 태그 내부의 CSS 코드는 셀렉터를 사용하여 모든 a 태그에 대해 스타일을 적용한다. 하지만 a 태그에 style 속성을 직접 사용하여 CSS 코드를 적용하면 해당 a 태그에 적용되는 스타일과 다른 a 태그들에 적용되는 스타일이 달라진다. HTML 태그에 style 속성을 사용하여 스타일을 적용하면 style 태그 내부의 셀렉터에서 나열한 스타일을 적용하지 않기 때문이다.

추가적으로 적용할 스타일을 작성한 것을 효과 또는 선언declaration이라고 한다. 적용할 효과가 여러개라면 다음과 같이 세미콜론으로 구분해야 한다.

```html
<style>
  a {
    color: black;           /* 효과 또는 선언 */
    text-decoration: none;  /* 효과 또는 선언 */
  }
</style>
```

셀렉터에서 뿐만 아니라 HTML 태그의 style 속성 내부에서도 마찬가지이다.

```html
<a href="2.html" style="color: red; text-decoration: underline;">CSS</a>
```

따라서 효과 뒤에 항상 세미콜론을 붙이는 것이 좋다.

## 혁명적 변화

CSS 문법을 이론적으로 정리한다. 예제 코드는 다음과 같다.

```css
a {
  color: red;
}
```

이 CSS 코드에서 사용한 것들을 부르는 용어가 있다.

- a - 셀렉터(Selector) 또는 선택자
- color: red - 선언(Declaration) 또는 효과
  - color - 프로퍼티(Property) 또는 속성
  - red - 프로퍼티 값(Property Value) 또는 속성 값

## CSS 속성을 스스로 알아내는 방법

h1 태그 내부에 있는 글씨의 크기를 키우고 싶다면 어떻게 할까? 다음과 같은 키워드를 검색할 수 있다.

- CSS
- text
- size
- property

검색 결과 **font-size** 라는 프로퍼티와 적용할 수 있는 프로퍼티 값을 확인할 수 있다.

```css
font-size: 50px;
```

그리고 h1 태그 내부에 있는 글씨를 가운데 정렬하고 싶으면 어떻게 할까? 다음과 같은 키워드를 검색할 수 있다.

- CSS
- text
- center
- property

검색 결과 **text-align** 이라는 프로퍼티와 적용할 수 있는 프로퍼티 값을 확인할 수 있다.

```css
text-align: center;
```

결과적으로 h1 태그에 적용할 프로퍼티이므로 h1 태그 셀렉터 내부에 효과를 작성한다.

```css
h1 {
  font-size: 50px;
  text-align: center;
}
```

이와 같은 방법으로 적용하려는 스타일을 담당하는 프로퍼티를 검색할 수 있다. 따라서 모든 프로퍼티를 암기해야 할 필요가 없다.

## CSS 선택자를 스스로 알아내는 방법

아래와 같이 디자인을 변경하려는 상황이다.
  1. 웹페이지의 모든 a 태그를 검은색으로 표시한다.
  2. 방문한 적이 있던 a 태그는 회색으로 표시한다.
  3. 현재 머물고 있는 a 태그는 빨간색으로 표시한다.

### 태그 선택자

첫 번째 상황으로, 웹페이지의 모든 a 태그를 검은색으로 표시하는 CSS 코드는 다음과 같다.

```css
a {
  color: black;
}
```

여기서 **a**는 웹페이지의 모든 a 태그를 선택한다는 **태그 선택자**이다.

### 클래스 선택자

두 번째 상황으로, 방문한 적이 있던 a 태그를 회색으로 표시하려면 어떻게 할까? HTML 예제 코드는 다음과 같다.

```html
<h1><a href="index.html">WEB</a></h1>
<ol>
  <li>
    <a href="1.html">HTML</a>
  </li>
  <li>
    <a href="2.html">CSS</a>
  </li>
  <li>
    <a href="3.html">JavaScript</a>
  </li>
</ol>
```

이 코드에서 HTML, CSS 링크를 이전에 봤다고 가정한다. 여기서 **class**라는 속성을 태그에 사용할 수 있다. 그리고 class 속성의 값으로 봤다는 의미의 "saw"를 사용한다.

```html
<h1><a href="index.html">WEB</a></h1>
<ol>
  <li>
    <a href="1.html" class="saw">HTML</a>
  </li>
  <li>
    <a href="2.html" class="saw">CSS</a>
  </li>
  <li>
    <a href="3.html">JavaScript</a>
  </li>
</ol>
```

saw라는 class의 값을 사용해서 디자인을 변경할 수 있다. 이때 class의 값 앞에 .(점)을 붙여야 한다는 것에 주의한다.

```css
.saw {
  color: gray;
}
```

**.saw**는 class의 값이 saw인 태그를 가리키는 **클래스 선택자**가 된다.

그런데 첫 번째 상황에서 a 태그 선택자를 사용해 효과를 적용하였고, 두 번째 상황에서 saw 클래스 선택자를 사용해 효과를 적용하였다.

```css
a {
  color: black;
}
.saw {
  color: gray;
}
```

이때 saw 클래스 선택자에 적용한 효과가 saw라는 값을 class의 값으로 갖는 태그에 적용되는 것을 확인할 수 있다. 이를 통해 태그 선택자보다 클래스 선택자가 우선한다는 것을 알 수 있다.

### id 선택자

세 번째 상황으로, 현재 머물고 있는 a 태그를 빨간색으로 표시하려면 어떻게 할까?

```html
<h1><a href="index.html">WEB</a></h1>
<ol>
  <li>
    <a href="1.html" class="saw">HTML</a>
  </li>
  <li>
    <a href="2.html" class="saw" id="active">CSS</a>
  </li>
  <li>
    <a href="3.html">JavaScript</a>
  </li>
</ol>
```

두 번째 a 태그를 현재 머물고 있는 a 태그라고 한다면 위에 있는 HTML 코드처럼 id라는 속성을 태그에 사용할 수 있다. 그리고 id 속성의 값으로 활성화되었다는 의미의 "active"를 사용하였다.

active라는 id의 값을 사용해서 디자인을 변경할 수 있다. 이때 id의 값 앞에 #을 붙어야 한다는 것에 주의한다.

```css
#acitve {
  color: red;
}
```

**#active**는 id의 값이 active인 태그를 가리키는 id 선택자가 된다.

그런데 두 번째 상황에서 saw 클래스 선택자를 사용해 효과를 적용하였고, 세 번째 상황에서 active id 선택자를 사용해 효과를 적용하였다.

```css
.saw {
  color: gray;
}
#active {
  color: red;
}
```

그리고 두 번째 a 태그에는 class 속성과 id 속성이 모두 사용되었다.

```html
<a href="2.html" class="saw" id="active">CSS</a>
```

이때 active id 선택자에 적용한 효과가 해당 태그에 적용되는 것을 확인할 수 있다. 이를 통해 클래스 선택자보다 id 선택자가 우선한다는 것을 알 수 있다.

### 선택자 우선순위

1. id 선택자
2. 클래스 선택자
3. 태그 선택자

id 속성의 값은 웹페이지에서 단 한 번만 등장해야 한다. id 속성의 값의 핵심은 중복돼서는 안 되는 유일무이한 값이라는 것이다.

웹페이지에서 모든 a 태그를 가리키는 a 태그 선택자와 웹페이지에서 중복되지 않는 유일한 active id 선택자 중에서 무엇이 더 구체적일까? 더 구체적인 선택자는 id 선택자이다. 태그 선택자는 id 선택자보다 포괄적이다.

id 선택자의 우선순위가 태그 선택자의 우선순위보다 높은 이유

  - 태그 선택자를 사용해 전체적인 태그의 디자인
  - 예외적인 태그들의 id를 찍어 가면서 id 선택자를 통해 예외를 두는 것이 디자인하는 데 훨씬 더 효율적

마찬가지로 클래스 선택자가 id 선택자보다 포괄적이고 태그 선택자보다 구체적이기 때문에 클래스 선택자의 우선순위는 id 선택자와 태그 선택자의 사이에 위치한다.

id 선택자, 클래스 선택자, 태그 선택자 말고도 여러 형태의 선택자들이 있다. 이것들의 사용법은 검색을 통해 알아가면 된다.

## 박스 모델

### block level element와 inline element

예제 코드는 아래와 같다.

```html
<h1>CSS</h1>Cascading Style Sheets (<a href="https://developer.mozilla.org/ko/docs/Web/CSS">CSS</a>) is a style sheet language used for describing the presentation of a document written in a markup language.
```

예제 코드를 확인하면 h1 태그는 화면 전체를 사용한다. h1 태그 이후 줄바꿈이 된다. 그런데 a 태그는 줄바꿈이 되지 않고 다른 컨텐츠들과 같은 라인에 위치하며 자기 컨텐츠만큼의 부피를 사용한다.

HTML의 여러 태그들은 그 태그의 성격과 일반적인 쓰임에 따라서 화면 전체를 쓰는 것과 자기 컨텐츠만큼의 부피를 갖는 것으로 나뉜다.

화면 전체를 사용하는 태그를 **block level element**라고 하고, 자기 컨텐츠만큼의 부피를 사용하는 태그를 **inline element**라고 한다.

**display** 프로퍼티를 사용하면 block level element와 inline element의 특징을 변경할 수 있다.

```css
h1 {
  /* h1 태그를 inline element로 사용하기 */
  display: inline;
}
a {
  /* a 태그를 block level element로 사용하기 */
  display: block;
}
```

### CSS의 박스 모델

CSS 박스 모델은 HTML 태그를 일종의 박스로 취급해서 박스의 부피감을 결정하는 것이고, 부피감을 결정하는 것은 디자인적으로 핵심적인 요소이다.

**padding** 프로퍼티
  - 컨텐츠와 테두리(border) 사이에 여백 설정하기

```css
h1 {
  padding: 20px;
}
```

**margin** 프로퍼티
  - 테두리(border) 바깥의 여백 설정하기

```css
h1 {
  padding: 20px;
  margin: 20px;
}
```

**border** 프로퍼티
  - padding과 margin 사이에 위치하는 테두리 설정하기

```css
h1 {
  border: 5px solid red;
  padding: 20px;
  margin: 20px;
}
```

**width** 프로퍼티
  - 태그의 너비 설정하기
  - 화면 전체를 사용하지 않도록 태그 너비 설정 가능

```css
h1 {
  border: 5px solid red;
  padding: 20px;
  margin: 20px;
  width: 100px;
}
```

### 박스 모델 써먹기

예제 코드는 다음과 같다.

```html
<body>
  <h1><a href="index.html">WEB</a></h1>
  <ol>
    <li><a href="1.html" class="saw">HTML</a></li>
    <li><a href="2.html" class="saw" id="active">CSS</a></li>
    <li><a href="3.html">JavaScript</a></li>
  </ol>
</body>
```

h1 태그에 border-bottom, margin, padding 프로퍼티를 사용하여 박스 모델을 적용한다.

```css
h1 {
  font-size: 50px;
  text-align: center;
  border-bottom: 1px solid gray;
  margin: 0px;
  padding: 20px;
}
```

ol 태그에 bottom-right, margin, padding, width 프로퍼티를 사용하여 박스 모델을 적용한다.

```css
ol {
  border-right: 1px solid gray;
  width: 100px;
  margin: 0px;
  padding: 20px;
}
```

body 태그에 기본적으로 설정된 margin 프로퍼티 값을 0으로 설정한다.

```css
body {
  margin: 0px;
}
```