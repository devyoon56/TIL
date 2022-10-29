# [WEB1 - HTML & Internet](https://opentutorials.org/course/3084, "생활코딩 WEB1 수업")

## 기본 문법 - 태그

아래 HTML 코드가 있다.

```html
Hypertext Markup Language (HTML) is the standard markup language for
<strong>creating <u>web</u> pages</strong> and web applications.
```

위 HTML 코드에서 사용한 태그는 다음과 같다.

- strong: 강조 표시 태그
- u: 밑줄 표시 태그

strong 태그를 사용한 것처럼 앞에 있는 태그를 열리는 태그, 뒤에 있는 태그를 닫히는 태그라고도 한다. 닫히는 태그의 경우 앞에 /를 붙인다.

또한 태그를 중첩해서 사용할 수 있다.

```html
<strong>creating <u>web</u> pages</strong>
```

위 코드에서 strong 태그 내부에 u 태그를 사용한 것을 보면, 태그를 중첩해서 사용하고 있다.

## 줄바꿈

아래는 예제 코드이다.

```html
<h1>HTML</h1>
Hypertext Markup Language (HTML) is the standard markup language for
<strong>creating <u>web</u> pages</strong> and web applications.Web browsers
receive HTML documents from a web server or from local storage and render them
into multimedia web pages. HTML describes the structure of a web page
semantically and originally included cues for the appearance of the document.

HTML elements are the building blocks of HTML pages. With HTML constructs,
images and other objects, such as interactive forms, may be embedded into the
rendered page. It provides a means to create structured documents by denoting
structural semantics for text such as headings, paragraphs, lists, links, quotes
and other items. HTML elements are delineated by tags, written using angle
brackets.
```

위 코드를 보면 단락 구분을 위해 줄바꿈을 했지만 브라우저의 결과는 그렇지 않다. 그 이유는 줄바꿈을 하려면 줄바꿈 태그를 사용해야 하기 때문이다. 줄바꿈 태그는 **br 태그** 이다.

br 태그의 특이한 점이 있다.

- 닫는 태그가 없음

HTML 여러 태그들 중에 무언가를 설명하지 않는 태그들은 감싸야할 컨텐츠가 없기 때문에 태그를 닫지 않는다는 규칙이 있다.

### 단락

위에서 br 태그를 사용한 이유는 단락을 표시하기 위함이다. 그런데 단락을 표현할 때 사용할 수 있는 **p** 태그가 있다. p 태그는 br 태그와 다르게 하나의 단락을 그룹핑하도록 열고 닫는 태그가 존재한다.

예제 코드를 다음과 같이 변경한다.

```html
<h1>HTML</h1>
<p>Hypertext Markup Language (HTML) is the standard markup language for
<strong>creating <u>web</u> pages</strong> and web applications.Web browsers
receive HTML documents from a web server or from local storage and render them
into multimedia web pages. HTML describes the structure of a web page
semantically and originally included cues for the appearance of the document.</p>
<p>HTML elements are the building blocks of HTML pages. With HTML constructs,
images and other objects, such as interactive forms, may be embedded into the
rendered page. It provides a means to create structured documents by denoting
structural semantics for text such as headings, paragraphs, lists, links, quotes
and other items. HTML elements are delineated by tags, written using angle
brackets.</p>
```

결과는 이전 코드와 거의 같지만 사용한 태그는 다르다. 그렇다면 어떤 태그를 사용해야 할까?

- 단락 표현 시 줄바꿈 태그보다 단락 표현 태그인 p 태그를 사용하는 것이 좋다.
- 그 이유는 단락에 단락 태그를 사용하는 것이 웹페이지를 정보로서 보다 가치있게 해주기 때문이다.
- br 태그는 단순히 줄바꿈을 의미할 뿐이다.

그런데 p 태그에는 단점이 있다.

- 단락과 단락의 간격이 고정되어 시각적인 자유도가 떨어진다.
- 반면 br 태그는 사용하는 만큼 줄바꿈되므로 원하는 만큼 간격을 줄 수 있는 장점이 있다.

하지만 CSS 기술을 사용하면 p 태그의 한계를 극복할 수 있다.

CSS를 이용해 두 단락의 간격을 조정해보자.

```html
<h1>HTML</h1>
<p>Hypertext Markup Language (HTML) is the standard markup language for
<strong>creating <u>web</u> pages</strong> and web applications.Web browsers
receive HTML documents from a web server or from local storage and render them
into multimedia web pages. HTML describes the structure of a web page
semantically and originally included cues for the appearance of the document.</p>
<p style="margin-top: 45px;">HTML elements are the building blocks of HTML pages. With HTML constructs,
images and other objects, such as interactive forms, may be embedded into the
rendered page. It provides a means to create structured documents by denoting
structural semantics for text such as headings, paragraphs, lists, links, quotes
and other items. HTML elements are delineated by tags, written using angle
brackets.</p>
```

```html
<p style="margin-top: 45px;">
```

p 태그에 style="margin-top: 45px;" 을 추가하면 p 태그 위쪽에 45px 만큼의 여백이 생긴다.

여기서 중요한 점.
- br 태그보다 p 태그가 좋은 이유를 이해하는 것
  - p 태그로 단락의 경계를 분명히 한다.
  - CSS로 p 태그의 디자인을 자유롭게 변경 가능하다.
  - 또한 이전에도 언급했듯이 단락에 단락 태그를 사용하는 것이 웹페이지를 정보로서 보다 가치있게 해준다.

## HTML이 중요한 이유

블로그에 글을 작성한다고 했을 때, HTML 태그를 아는 사람과 일반인이 만든 코드 차이를 보자.

```html
<h3>coding</h3>
```
HTML 태그를 아는 사람의 코드는 coding이 제목이라는 의미를 갖는다.

```html
<strong><span style="font-size:22px;">coding</span></strong>
```
일반인의 코드는 coding이 22px의 크기를 갖고, 진하게 표시되어야 한다는 시각적 장식만 갖고 있다. 어디에도 제목이라는 정보는 없다.

두 코드는 시각적인 결과로 동일하다. 하지만 코드는 완전히 다르다. 코드가 다른 것은 중요한 의미를 갖는다.

누구의 코드가 더 좋은지 검색엔진을 통해 알 수 있다.
  - 검색엔진은 전세계 웹페이지를 분석한다.
  - 사용자가 검색 했을 때 검색 결과를 출력한다.
  - 만약 검색엔진에 'coding'이라는 정보를 검색한다면,
  - 검색엔진은 h3 태그로 감싸진 페이지를 더 먼저 보여줄 것이다.
  - h3 태그는 제목을 의미하기 때문이다.

### 접근성(accessibility)

위에서 언급한 이유 뿐만 아니라 HTML이 중요한 이유가 또 하나 있다.

웹의 핵심 철학은 **접근성**이다.

웹은 모든 운영체제에서 동작하고, 웹페이지의 소스코드는 누구나 볼 수 있고, 웹은 저작권이 없는 순수한 공공재이다. 웹의 이런 특징들이 웹을 다른 기술들과 구별하는 특별한 것으로 만들 수 있다.

여기에 더해서 누구나 차별없이 정보에 접근할 수 있어야 한다는 철학을 접근성이라고 한다.

특히 웹이 중요하게 생각하는 접근성은 신체적 장애가 있는 사람도 웹을 통해 정보에 접근할 수 있어야 한다는 것이다.

- 시각장애인들은 스크린 리더 같은 프로그램으로 정보를 청각화해서 접한다.
- 만약 웹페이지를 이쁘게 꾸미기 위해 웹페이지 전체를 이미지로 만든다면 시각장애인들은 정보를 접할 수 없다.

반대로, HTML을 의미론적으로 잘 사용하면 누군가에게 정말 큰 도움을 주는 것이다.

## 최후의 문법 속성과 img

이미지를 넣으려면 img 태그를 사용한다. 예제 코드는 다음과 같다.

```html
<h1>HTML</h1>
<p>Hypertext Markup Language (HTML) is the standard markup language for <strong>creating <u>web</u> pages</strong> and web applications.Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. HTML describes the structure of a web page semantically and originally included cues for the appearance of the document.
<img>
</p><p style="margin-top:45px;">HTML elements are the building blocks of HTML pages. With HTML constructs, images and other objects, such as interactive forms, may be embedded into the rendered page. It provides a means to create structured documents by denoting structural semantics for text such as headings, paragraphs, lists, links, quotes and other items. HTML elements are delineated by tags, written using angle brackets. </p>
```

img 태그를 사용했는데도 결과는 보이지 않는다. 어떤 이미지를 불러올 지에 대한 정보가 없기 때문이다.

태그 이름만으로 정보가 부족한 경우, 속성(attribute)을 사용해야 한다.

img 태그에 src를 붙여서 아래와 같이 작성한다.

```html
<h1>HTML</h1>
<p>Hypertext Markup Language (HTML) is the standard markup language for <strong>creating <u>web</u> pages</strong> and web applications.Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. HTML describes the structure of a web page semantically and originally included cues for the appearance of the document.
<img src="https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7648.png">
</p><p style="margin-top:45px;">HTML elements are the building blocks of HTML pages. With HTML constructs, images and other objects, such as interactive forms, may be embedded into the rendered page. It provides a means to create structured documents by denoting structural semantics for text such as headings, paragraphs, lists, links, quotes and other items. HTML elements are delineated by tags, written using angle brackets. </p>
```

```html
<img src="https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7648.png">
```

src가 바로 속성이다. 그리고 속성의 값인 주소는 이미지의 주소이다.

src 속성을 사용해 이미지를 불러올 수 있게 되었다.

이 이미지는 인터넷에 있는 이미지인데, 로컬에 저장된 이미지를 표시할 수도 있다.

  - 웹페이지 파일과 같은 위치에 이미지 파일을 저장한다.
  - src 속성 값으로 이미지 파일의 이름을 사용한다.

```html
<img src="conding.avif">
```

이와 같이 속성은 태그 이름만으로 정보가 부족할 때 사용한다.

## 부모 자식과 목록

태그의 관계를 나타내는 표현인 부모(parent), 자식(child)에 대해 알아보자.

아래 코드를 보자.(parent, child 태그는 없는 태그)

```html
<parent>
  <child></child>
</parent>
```

parent 태그에 대해 child 태그를 자식 태그라고 한다.

또한 child 태그에 대해 parent 태그를 부모 태그라 한다.

아래 코드를 보면 p 태그가 a 태그의 부모, a 태그가 p 태그의 자식이다.

```html
<p>
    <a href="https://opentutorials.org">opentutorials</a>
</p>
```

그런데 a 태그는 반드시 p 태그의 자식이어야 하는 것은 아니다.

p 태그도 a 태그의 부모일 필요는 없다.

하지만 몇몇 태그들은 부모 자식 관계처럼 고정 관계인 태그들이 있다.

예제에 목차를 추가하자.

```html
1. HTML<br>
2. CSS<br>
3. JavaScript<br>
```

그런데 목차를 표현하기 위해 사용하는 태그가 있다.

목차를 표현하는 태그는 li 태그이다.

```html
<li>1. HTML</li>
<li>2. CSS</li>
<li>3. JavaScript</li>
```

참가자 목록도 추가해보자.

```html
<li>1. HTML</li>
<li>2. CSS</li>
<li>3. JavaScript</li>

<li>egoing</li>
<li>k8805</li>
<li>sorialgi</li>
```

브라우저 결과, 목차와 참가자 목록이 구분되지 않는다.

목록은 다른 목록과 구분할 수 있도록 어떤 경계가 필요한데, 이 때 ul 태그를 사용한다.

```html
<ul>
  <li>1. HTML</li>
  <li>2. CSS</li>
  <li>3. JavaScript</li>
</ul>
<ul>
  <li>egoing</li>
  <li>k8805</li>
  <li>sorialgi</li>
</ul>
```

li 태그는 ul 태그를 꼭 필요로 한다. ul 태그 역시 li 태그가 없다면 존재 가치가 없다.

위 코드에서 수업 목록을 보자.

만약 수업 목록이 3개가 아니라 1억개라면 어떨까? 누군가 저 첫 번째 항목을 지워달라고 한다면 어떻게 해야할까?

나머지 항목의 모든 번호를 수정해야 할 것이다.

예제를 다음과 같이 변경하자.

```html
<ol>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ol>
```

ul 태그를 ol 태그로 변경하였다.

ul은 unordered list의 약자이고,

ol은 ordered list의 약자이다.

## 문서의 구조와 슈퍼스타들

정보가 많아지면서 정보를 잘 정리정돈하기 위한 체계, 다시 말해 구조라는 것이 필요하다.

웹페이지 제목을 지정하려면 title 태그를 사용한다.

```html
<title>WEB1 - html</title>
```

title 태그의 경우, 검색엔진이 웹페이지를 분석할 때 가장 중요하게 생각하는 태그이다.

또한, 영어가 아닌 문자로 웹페이지를 만들면 문자가 깨지는 경우가 있다.

웹페이지를 UTF-8로 저장했다면 웹페이지를 열 때도 UTF-8 방식으로 해석해서 열어야 한다.

영어가 아닌 문자가 깨지는 이유는
  - 웹페이지가 저장된 문자 표현 방식과
  - 웹브라우저가 웹페이지를 해석하는 방식이 일치하지 않을 때

이다.

이 문제를 해결하려면 아래 코드처럼 웹브라우저에게 이 웹페이지를 UTF-8로 열어달라고 해야 한다.

```html
<title>WEB1 - html</title>
<meta charset="utf-8">
```

위 두 줄의 코드는 본문이 아니고 본문을 설명하는 코드이다.

HTML 개발자들은 본문과 본문을 설명하는 정보를 각기 다른 태그로 분리해서 정리 정돈하기로 하였다.

본문은 body 태그를,

본문을 설명하는 태그는 head 태그를 사용한다.

```html
<head>
  <title>WEB1 - html</title>
  <meta charset="utf-8" />
</head>
<body>
  <ol>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
  </ol>
  <h1>HTML</h1>
  <p>
    Hypertext Markup Language (HTML) is the standard markup language for
    <strong>creating <u>web</u> pages</strong> and web applications.Web browsers
    receive HTML documents from a web server or from local storage and render
    them into multimedia web pages. HTML describes the structure of a web page
    semantically and originally included cues for the appearance of the
    document.
    <img src="coding.avif" />
  </p>
  <p style="margin-top: 45px">
    HTML elements are the building blocks of HTML pages. With HTML constructs,
    images and other objects, such as interactive forms, may be embedded into
    the rendered page. It provides a means to create structured documents by
    denoting structural semantics for text such as headings, paragraphs, lists,
    links, quotes and other items. HTML elements are delineated by tags, written
    using angle brackets.
  </p>
</body>
```

또한 body 태그와 head 태그를 감싸는 하나의 태그가 있다.

html 태그이다.

또한 웹페이지가 HTML로 만들어졌다는 것을 표현하기 위해 문서 시작에 아래 코드를 추가한다.

```html
<!doctype html>
```

결과적으로 아래와 같이 웹페이지의 구조를 완성하였다.

```html
<!doctype html>
<html>
  <head>
    <title>WEB1 - html</title>
    <meta charset="utf-8" />
  </head>

  <body>
    <ol>
      <li>HTML</li>
      <li>CSS</li>
      <li>JavaScript</li>
    </ol>
    <h1>HTML</h1>
    <p>
      Hypertext Markup Language (HTML) is the standard markup language for
      <strong>creating <u>web</u> pages</strong> and web applications.Web
      browsers receive HTML documents from a web server or from local storage
      and render them into multimedia web pages. HTML describes the structure of
      a web page semantically and originally included cues for the appearance of
      the document.
      <img src="coding.avif" />
    </p>
    <p style="margin-top: 45px">
      HTML elements are the building blocks of HTML pages. With HTML constructs,
      images and other objects, such as interactive forms, may be embedded into
      the rendered page. It provides a means to create structured documents by
      denoting structural semantics for text such as headings, paragraphs,
      lists, links, quotes and other items. HTML elements are delineated by
      tags, written using angle brackets.
    </p>
  </body>
</html>
```

## HTML 태그의 제왕

HTML의 약자 HyperText Markup Language의 HyperText가 이 태그를 의미한다.

이 태그의 이름은 anchor의 첫글자 a이다.

a 태그의 역할은 바로 **링크**이다.

예제 코드의 텍스트 Hypertext Markup Language (HTML) 에 링크를 걸어보자.

```html
<a href="https://www.w3.org/TR/html5/" target="_blank" title="html5 specification">Hypertext Markup Language (HTML)</a>
```

href는 <u>H</u>yperText <u>Ref</u>erence의 약자이다.

target="_blank"는 링크 클릭 시 새창에서 페이지가 열리게 하는 속성이다.

또 title은 이 링크가 어떤 내용을 담고 있는지 툴팁으로 보여주는 기능이다.

## 웹사이트 완성

페이지가 모이면 책이 되듯이 웹페이지를 링크로 모으면 일종의 책이 만들어진다.

링크를 통해 서로 결합되어 있는 웹페이지들의 그룹을 웹에서는 웹사이트(web site)라고 한다.

웹사이트를 만들기 위해 웹페이지 전체를 대표하는 큰 제목을 만든다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7701.png)

그리고 각 부분에 링크를 걸어서 다른 페이지와 연결시킨다. 아래 그림에서 파일명은 링크로 연결될 웹페이지의 파일명이다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7702.png)

먼저 1.html 의 내용을 수정하고 링크를 건다.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>WEB1 - HTML</title>
    <meta charset="utf-8" />
  </head>

  <body>
    <h1><a href="index.html">WEB</a></h1>
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <h2>HTML</h2>
    <p>
      <a href="https://www.w3.org/TR/html5/"
        >Hypertext Markup Language (HTML)</a
      >
      is the standard markup language for
      <strong>creating <u>web</u> pages</strong> and web applications.Web
      browsers receive HTML documents from a web server or from local storage
      and render them into multimedia web pages. HTML describes the structure of
      a web page semantically and originally included cues for the appearance of
      the document.
      <img src="coding.avif" />
    </p>
    <p style="margin-top: 45px">
      HTML elements are the building blocks of HTML pages. With HTML constructs,
      images and other objects, such as interactive forms, may be embedded into
      the rendered page. It provides a means to create structured documents by
      denoting structural semantics for text such as headings, paragraphs,
      lists, links, quotes and other items. HTML elements are delineated by
      tags, written using angle brackets.
    </p>
  </body>
</html>
```

1.html 파일을 복제해서 index.html, 2.html, 3.html을 생성한다.

그리고 각각의 파일에 맞게 수정한다.

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>WEB1 - Welcome</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1><a href="index.html">WEB</a></h1>
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <h2>WEB</h2>
    <p>
      The World Wide Web (abbreviated WWW or the Web) is an information space
      where documents and other web resources are identified by Uniform Resource
      Locators (URLs), interlinked by hypertext links, and can be accessed via
      the Internet.[1] English scientist Tim Berners-Lee invented the World Wide
      Web in 1989. He wrote the first web browser computer program in 1990 while
      employed at CERN in Switzerland.[2][3] The Web browser was released
      outside of CERN in 1991, first to other research institutions starting in
      January 1991 and to the general public on the Internet in August 1991.
    </p>
  </body>
</html>
```

```html
<!-- 1.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>WEB1 - HTML</title>
    <meta charset="utf-8" />
  </head>

  <body>
    <h1><a href="index.html">WEB</a></h1>
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <h2>HTML</h2>
    <p>
      <a href="https://www.w3.org/TR/html5/"
        >Hypertext Markup Language (HTML)</a
      >
      is the standard markup language for
      <strong>creating <u>web</u> pages</strong> and web applications.Web
      browsers receive HTML documents from a web server or from local storage
      and render them into multimedia web pages. HTML describes the structure of
      a web page semantically and originally included cues for the appearance of
      the document.
      <img src="coding.avif" />
    </p>
    <p style="margin-top: 45px">
      HTML elements are the building blocks of HTML pages. With HTML constructs,
      images and other objects, such as interactive forms, may be embedded into
      the rendered page. It provides a means to create structured documents by
      denoting structural semantics for text such as headings, paragraphs,
      lists, links, quotes and other items. HTML elements are delineated by
      tags, written using angle brackets.
    </p>
  </body>
</html>
```

```html
<!-- 2.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>WEB1 - CSS</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1><a href="index.html">WEB</a></h1>
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <h2>CSS</h2>
    <p>
      Cascading Style Sheets (CSS) is a style sheet language used for describing
      the presentation of a document written in a markup language. Although most
      often used to set the visual style of web pages and user interfaces
      written in HTML and XHTML, the language can be applied to any XML
      document, including plain XML, SVG and XUL, and is applicable to rendering
      in speech, or on other media. Along with HTML and JavaScript, CSS is a
      cornerstone technology used by most websites to create visually engaging
      webpages, user interfaces for web applications, and user interfaces for
      many mobile applications.
    </p>
  </body>
</html>
```

```html
<!-- 3.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>WEB1 - JavaScript</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1><a href="index.html">WEB</a></h1>
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <h2>JavaScript</h2>
    <p>
      JavaScript (/ˈdʒɑːvəˌskrɪpt/[6]), often abbreviated as JS, is a
      high-level, dynamic, weakly typed, prototype-based, multi-paradigm, and
      interpreted programming language. Alongside HTML and CSS, JavaScript is
      one of the three core technologies of World Wide Web content production.
      It is used to make webpages interactive and provide online programs,
      including video games. The majority of websites employ it, and all modern
      web browsers support it without the need for plug-ins by means of a
      built-in JavaScript engine. Each of the many JavaScript engines represent
      a different implementation of JavaScript, all based on the ECMAScript
      specification, with some engines not supporting the spec fully, and with
      many engines supporting additional features beyond ECMA.
    </p>
  </body>
</html>
```

아주 간단한 웹사이트가 완성되었다.

## 원시웹

인터넷과 웹은 같을까? 다를까?

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7720.png)

인터넷과 웹이 어떻게 다른지 비유적으로 알아보자.

- 인터넷이 웹이라면 웹은 도시 위에 있는 건물 하나이다.
- 인터넷이 도로라면 웹은 도로 위를 달리는 자동차 한 대이다.
- 인터넷이 운영체제라면 웹은 운영체제 위에서 동작하는 하나의 앱이다.

웹은 인터넷의 부분집합이다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7724.png)

정보기술 역사의 중요한 사건 2개

- 인터넷의 탄생: 1960년
- 웹의 탄생: 1990년

인터넷과 웹을 잘 구분하지 못하는 이유

- 웹의 성공
- 웹 때문에 사람들이 인터넷을 사용하기 시작

인터넷의 시작

- 통신 시스템의 중앙집중화
- 외부 공격 시 통신 시스템의 마비 위험
- 분산된 형태의 통신 시스템 구상

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7730.jpeg)

팀 버너스 리

- 웹의 창시자
- 웹페이지 편집 프로그램 개발
- 세계 최초의 웹브라우저 월드 와이드 웹(world wide web) 개발 -> 훗날 웹의 이름으로 사용됨
- 웹 서버 완성 후 info.cern.ch 도메인 네임 부여 -> 세계 최초의 웹페이지

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7742.png)

## 인터넷을 여는 열쇠: 서버와 클라이언트

인터넷이 동작하는 기본 원리를 알아보자.

인터넷이 동작하려면 최소 컴퓨터 2대는 있어야 한다.

팀 버너스 리는 인터넷을 이용해서 웹을 만들기로 한다. 이를 위해 인터넷으로 연결된 2대의 컴퓨터를 장만한다.

그리고 웹브라우저와 웹서버라는 프로그램을 개발한다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7751.jpeg)

웹서버가 설치된 컴퓨터
- info.cern.ch라는 주소 부여
- 컴퓨터의 어떤 디렉토리에 index.html이라는 파일을 저장

웹브라우저가 설치된 컴퓨터
- 주소창에 http://info.cern.ch/index.html 이라는 주소 입력 후 엔터

웹브라우저에서 주소를 입력하고 엔터를 치면 어떤 일이 일어날까?

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7752.jpeg)

- 웹브라우저가 설치된 컴퓨터는 인터넷을 통해 info.cern.ch라는 주소의 컴퓨터에게 전기적 신호를 보냄
- 이 때 전기적 신호의 내용은 '나는 index.html이라는 파일의 코드를 원합니다'
- info.cern.ch에 설치된 웹서버 프로그램이 어떤 디렉터리에서 index.html이라는 파일을 탐색
- 파일 내용을 읽어 전기적 신호로 바꾸어 웹브라우저가 설치된 컴퓨터에 전달
- 웹브라우저가 설치된 컴퓨터에 index.html 코드가 도착
- 웹브라우저는 코드를 읽어 웹페이지를 화면에 출력

웹브라우저가 설치된 컴퓨터와 웹서버가 설치된 컴픁터는 서로 정보를 주고 받는다.

웹브라우저가 설치된 컴퓨터는 정보를 요청하고, 웹서버가 설치된 컴퓨터는 정보를 응답한다.

요청하는 컴퓨터를 클라이언트 컴퓨터, 응답하는 컴퓨터를 서버 컴퓨터로 부르기로 한다.

## 웹호스팅 Github pages

웹호스팅
- 웹서버를 전문적으로 빌려주는 서비스

웹호스팅 업체
- 웹서버를 전문적으로 빌려주는 비즈니스 업체

깃헙이 제공하는 여러 기능 중 웹호스팅 기능을 이용해서 홈페이지를 운영해보자.

1. 'web1'이라는 저장소를 생성한다.
2. 이전에 작업한 파일들을 저장소에 업로드한다.
3. 저장소의 Settings 버튼을 선택한다.
4. 사이드바에서 Pages를 선택한다.
5. Branch를 main으로 선택하고 Save 버튼을 누른다.
![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/12692.png)
6. 주소가 표시된다.
7. 주소에 방문하면 웹페이지를 볼 수 있다.

![](https://user-images.githubusercontent.com/75947656/198823768-04f182b0-046b-45b5-9485-237b89cd829f.png)

이 과정들을 이론적으로 정리해보자.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7777.jpeg)

my는 내 컴퓨터, visitor는 웹페이지를 보고 싶어하는 사람이다.

여기서 깃헙의 pages 기능을 이용했다. 깃헙에 파일들을 업로드하고, pages 기능을 활성화하면 깃헙의 서버 컴퓨터에 웹서버가 켜진다. 그리고 우리에게 웹서버의 주소를 알려준다.

이제 웹서버의 주소를 방문자에게 알려주면 방문자는 내 컴퓨터가 아닌 깃헙의 컴퓨터에 설치된 웹서버에 접속하게 된다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/7778.jpeg)

웹서버를 직접 운영하는 것에 비해 웹호스팅을 이용하면 쉽다. 하지만 인터넷의 원리가 감춰진다.

## 웹서버 운영하기 Web Server for Chrome

Web Server for Chrome은 크롬 확장 기능으로서 설치되는 프로그램이다.

1. 크롬 브라우저에서 Web Server for Chrome 확장 프로그램을 설치 후 실행한다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/course/3084/12700.jpg)

2. 누군가 웹서버에 접속했을 때 어느 디렉터리에서 파일을 찾을지 알려줘야 한다.
    
    - 2번 CHOOSE FOLDER를 선택하고 프로젝트 폴더를 선택한다.
    - 웹서버는 이 폴더 안에서만 요청한 파일을 찾아 응답한다.

3. 1번 스위치를 오른쪽으로 이동하면 웹서버가 실행된다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/course/3084/12702.jpg)

  - Web Server URL(s)의 http://127.0.0.1:8887 주소를 확인한다.

4. 이 주소를 웹브라우저 주소창에 입력하여 결과를 확인한다.

![](https://user-images.githubusercontent.com/75947656/198824584-b1e79b57-0733-43c6-84db-5598b2b251e8.png)

### 웹서버를 통해 웹페이지를 여는 것과 파일 찾기를 통해 웹페이지를 여는 것의 차이

주소를 비교해보자.

- 파일 찾기: file///Desktop/web/index.html
- 웹서버: http://127.0.0.1:8887/index.html

그림은 다음과 같다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/12707.jpg)

웹서버로 접속한 주소를 자세히 알아보자.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/12708.jpg)

- http: http는 웹페이지를 주고받기 위한 통신 규약인 http를 이용해서 통신하겠다는 의미
- 127.0.0.1: Internet Protocol Address로서, 인터넷에서 상용하는 주소를 의미
  - IP Address는 0.0.0.0 부터 255.255.255.255 까지의 주소가 존재
  - 127.0.0.1 은 내 컴퓨터 자신을 가리키는 특별한 주소를 의미
- Port는 넘어가도록 하자

그런데 같은 컴퓨터에 설치된 웹브라우저와 웹서버가 정보를 주고받는 것은 현실의 웹과 다르다.

서로 다른 컴퓨터끼리 정보를 주고 받을 수 있어야 한다.

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/3135/12709.png)

스마트폰을 이용해 스마트폰의 웹브라우저와 내 컴퓨터에 설치된 웹서버가 서로 통신할 수 있게 해보자.

1. 스마트폰과 컴퓨터를 같은 네트워크에 연결한다.
2. 웹서버를 일단 끄고, Accessible on local network 옵션을 켠다.
3. 웹서버를 다시 켜서 옵션을 반영한다.
4. 새로운 아이피 주소를 확인한다.
  - 이 주소가 같은 네트워크에서 사용할 수 있는 웹서버가 설치된 컴퓨터의 IP 주소이다.
  - http://192.168.35.173:8887
5. 스마트폰의 웹브라우저에서 주소를 입력해서 결과를 확인한다.

## 코드의 힘 - 동영상 삽입

HTML iframe 태그를 사용하면 웹페이지에 동영상을 삽입할 수 있다.

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/jSJM9iOiQ1g" frameborder="0" allowfullscreen></iframe>
```

1.html 코드에 위 코드를 추가한 결과 아래와 같이 유튜브 동영상이 웹페이지에 삽입되었고 재생할 수도 있다.

![](https://user-images.githubusercontent.com/75947656/198829196-d96aed82-258d-4717-aeae-e8f3b31184b6.png)

## 코드의 힘 - 댓글 기능 추가

Disqus를 등록하여 블로그에 댓글 기능을 추가할 수 있다.

댓글 기능을 추가하려는 웹페이지에 아래 코드를 추가한다.

```html
<p>
  <div id="disqus_thread"></div>
  <script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    /*
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://web1-gxxpb73xzn.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
  </script>
  <noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</p>
```

기능이 정상적으로 동작하는지 확인하려면 파일 경로를 사용하면 안돼고

이전에 사용한 Web Server for Chrome 확장 프로그램으로 웹서버를 동작시켜서 IP 주소에 접근해야 한다.

![](https://user-images.githubusercontent.com/75947656/198830016-86b9300e-9f47-4b10-bd96-55f10fc3236c.png)

## 코드의 힘 - 채팅 기능 추가

tawk.to의 채팅 위젯을 사용하면 블로그에 채팅 기능을 추가할 수 있다.

댓글 기능을 추가하려는 웹페이지에 아래 코드를 추가한다.

```html
<p>
  <!--Start of Tawk.to Script-->
  <script type="text/javascript">
  var Tawk_API=Tawk_API||{}, Tawk_LoadStart=new Date();
  (function(){
  var s1=document.createElement("script"),s0=document.getElementsByTagName("script")[0];
  s1.async=true;
  s1.src='https://embed.tawk.to/635d1530b0d6371309cc2f5b/1gghplic0';
  s1.charset='UTF-8';
  s1.setAttribute('crossorigin','*');
  s0.parentNode.insertBefore(s1,s0);
  })();
  </script>
  <!--End of Tawk.to Script-->
</p>
```

댓글 기능과 마찬가지로 파일 경로를 사용하면 안돼고

Web Server for Chrome 확장 프로그램으로 웹서버를 동작시켜서 IP 주소에 접근해야 한다.

![](https://user-images.githubusercontent.com/75947656/198830241-12b24ea1-76cb-4e73-8df6-bfabd2726327.png)

## 코드의 힘 - 웹사이트 방문자 분석기

구글 애널리틱스를 삽입하는 코드를 웹페이지에 추가하면 구글 애널리틱스에서 웹사이트에 방문한 방문자를 분석한 데이터를 제공한다.

아래 코드를 head 태그 내부에 삽입한다.

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-SFYLRR75W6"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-SFYLRR75W6');
</script>
```

여기서는 깃헙 웹호스팅 pages 기능을 활용하는 저장소에 코드에 해당 기능을 추가하였다.

![](https://user-images.githubusercontent.com/75947656/198831058-f1ad2d80-2a4e-407b-bc96-bfb5c9e4257e.png)

https://devyoon56.github.io/web1/1.html 웹페이지에 방문한 결과로,

구글 애널리틱스에서 사용자 수가 1이 증가한 것을 확인할 수 있다.