# WEB2 - Node.js

# Node.js로 웹서버 만들기

Node.js는 웹 서버로 사용할 수 있다. Node.js가 웹 서버 기능을 내장하고 있기 때문이다.

Node.js를 웹 서버로 사용하는 코드

```js
var http = require("http");
var fs = require("fs");
var app = http.createServer(function (request, response) {
  var url = request.url;
  if (request.url == "/") {
    url = "/index.html";
  }
  if (request.url == "/favicon.ico") {
    response.writeHead(404);
    response.end();
    return;
  }
  response.writeHead(200);
  response.end(fs.readFileSync(__dirname + url));
});
app.listen(3000);
```

- 프로그래밍적으로 사용자에게 전송할 데이터를 생성하는 코드이다.
- 지금은 대략적으로만 이렇게 알고 넘어가자.

main.js 자바스크립트 파일에 코드를 넣고 터미널에서 해당 파일을 Node.js로 실행시킨다.

```
node main.js
```

웹브라우저 주소창에 localhost:3000 을 입력하여 결과를 확인한다.

# 자바스크립트 문법 - Number Data type

자바스크립트는 숫자 값에 대해 number 데이터 타입을 제공한다.

```js
console.log(1 + 1); // 2
console.log(1 - 1); // 0
console.log(2 * 2); // 4
console.log(10 / 2); // 5
```

# 자바스크립트 문법 - String

자바스크립트는 문자열에 대해 string 데이터 타입을 제공한다.

문자열의 경우 작은 따옴표와 큰 따옴표를 모두 사용할 수 있고, 항상 짝을 맞춰 사용해야 한다.

```js
console.log("1" + "1"); // 11
console.log("javascript".length); // 10
```

- 문자열 덧셈의 경우, 덧셈이 결합 연산자가 되어 문자열을 결합한다.
- 문자열의 개수를 세려면 length 프로퍼티를 사용한다.

# 자바스크립트 문법 - 변수의 형식

```js
var a = 1;
console.log(a); // 1

a = 2;
console.log(a); // 2
```

- 변수를 선언할 때 var 키워드를 사용한다.
- 대입 연산자(=)로 변수에 값을 대입한다.
- 이미 선언된 변수에는 var 키워드를 사용하지 않는다.

# 자바스크립트 문법 - 변수의 활용

변수를 사용한다는 것에 여러 의미가 있다.

```js
var letter = "Lorem ipsum dolor sit amet, consectetur adipiscing elit.";
console.log(letter);
```

- letter라는 데이터의 이름을 보고 데이터가 무엇을 의미하는지를 추론할 수 있다.

```js
var name = "egoing";
var letter =
  "Dear " +
  name +
  " Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse vestibulum scelerisque erat, ac viverra ligula feugiat ut. Morbi malesuada finibus venenatis. Suspendisse malesuada pellentesque turpis," +
  name +
  " sit amet iaculis ipsum bibendum commodo. Curabitur dictum erat sit amet fringilla rhoncus. Nam dolor nunc, auctor lobortis ex nec, semper pretium lorem. Sed luctus, leo quis vestibulum pretium, risus elit accumsan urna, aliquet venenatis sem libero at justo." +
  name +
  " Nunc tempus suscipit commodo.";
console.log(letter);
```

- name 변수가 항상 같다는 것을 확신할 수 있기 때문에 가독성이 좋아진다.
- name 변수의 값을 바꾸면 name 변수가 사용된 모든 곳에서 값이 바뀐다.

# 자바스크립트 문법 - 템플릿 리터럴

```js
var name = "egoing";
var letter = `Dear ${name} Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse vestibulum scelerisque erat, ac viverra ligula feugiat ut. Morbi malesuada finibus venenatis. ${name} Suspendisse malesuada pellentesque turpis, sit amet iaculis ipsum bibendum commodo. Curabitur dictum erat sit amet fringilla rhoncus. Nam dolor nunc, auctor lobortis ex nec, semper pretium lorem. Sed luctus, leo quis vestibulum pretium, risus elit accumsan urna, aliquet venenatis sem libero at justo. ${name} Nunc tempus suscipit commodo.`;
console.log(letter);
```

- 템플릿 리터럴은 백틱(``)과 ${}를 사용한다.
- 백틱(``) 내부에 문자열을 입력하고, ${} 내부에 변수를 입력하면 변수의 값이 문자열로 치환된다.

# URL의 이해

URL 샘플

http://opentutorials.org:3000/main?id=HTML&page=12

  - **http**
    - protocol, 프로토콜, 통신 규칙
    - 사용자가 서버에 접속할 때 어떤 방식으로 통신할 것인지를 나타낸다.
    - http는 웹브라우저와 웹서버가 서로 데이터를 주고 받기 위해 만들어진 통신 규칙이다.
  - **opentutorials.org**
    - host 또는 domain name
    - 인터넷에 연결된 특정 컴퓨터의 주소이다.
  - **3000**
    - 포트 번호
    - 한 대의 컴퓨터에 여러 서버가 있을 수 있는데, 클라이언트가 서버에 접속했을 때 어떤 서버와 통신할지가 애매하다.
    - 클라이언트가 서버에 접속할 때 포트번호를 명시하면 해당 포트번호에 연결된 서버와 통신하게 된다.
  - **main**
    - path
    - 컴퓨터 안에 있는 어떤 디렉터리의 어떤 파일인지를 가리킨다.
  - **id=HTML&page=12**
    - query string
    - 서버에게 정보를 전달한다. 예를 들어 원하는 정보가 HTML이고 페이지는 12이다.
    - query string은 물음표(?)로 시작하는 걸로 약속되어 있다.
    - 값과 값은 앰퍼센드(&)를 쓰기로 약속되어 있다.
    - 값의 이름과 값은 =로 구분하기로 약속되어 있다.

# URL을 통해서 입력된 값 사용하기

http://localhost/?id=HTML

이 주소로 사용자가 웹 애플리케이션에 접속했을 때 id 값이 무엇이냐에 따라 사용자에게 적당한 컨텐츠를 보여주려고 한다.

  - URL에서 id가 위치하는 부분을 query string이라고 한다.
  - Query string에 따라 다른 정보를 보여주려는 것이다.

Query string에 따라 다른 정보를 보여주려면 URL을 분석해서 query string을 추출해야 한다.

  - 키워드: nodejs url parse query string

main.js 코드

```js
var http = require("http");
var fs = require("fs");
var url = require("url");

var app = http.createServer(function (request, response) {
  var _url = request.url;
  var queryData = url.parse(_url, true).query;
  console.log(queryData.id);

  if (_url == "/") {
    _url = "/index.html";
  }
  if (_url == "/favicon.ico") {
    response.writeHead(404);
    response.end();
    return;
  }
  response.writeHead(200);
  response.end(queryData.id);
});
app.listen(3000);
```

- 웹 애플리케이션을 실행하고, 웹브라우저 주소창에 localhost:3000/?id=HTML을 입력한다.
- 결과를 확인하면 에러가 발생하지만, queryData가 객체인 것을 확인할 수 있다.
  - { id: 'HTML' }
  - queryData에는 query string이 객체로 들어온다는 것을 알 수 있다.
  - queryData.id 확인 결과 HTML인 것을 알 수 있다.
- **response.end(queryData.id)** 코드를 통해 query string에 따라 다른 정보를 웹페이지에 출력한다.
  - id=HTML 이면 단순히 HTML이 출력된다.
  - id=CSs 이면 단순히 CSS가 출력된다.

# App 제작 - 동적인 웹페이지 만들기

Query string에 따라 동적으로 웹페이지를 출력하려고 한다.

main.js 코드

```js
var http = require("http");
var fs = require("fs");
var url = require("url");

var app = http.createServer(function (request, response) {
  var _url = request.url;
  var queryData = url.parse(_url, true).query;
  var title = queryData.id;
  if (_url == "/") {
    title = "Welcome";
  }
  if (_url == "/favicon.ico") {
    response.writeHead(404);
    response.end();
    return;
  }
  response.writeHead(200);
  var template = `
    <!doctype html>
    <html>
    <head>
      <title>WEB1 - ${title}</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1>
      <ol>
        <li><a href="/?id=HTML">HTML</a></li>
        <li><a href="/?id=CSS">CSS</a></li>
        <li><a href="/?id=JavaScript">JavaScript</a></li>
      </ol>
      <h2>${title}</h2>
      <p><a href="https://www.w3.org/TR/html5/" target="_blank" title="html5 speicification">Hypertext Markup Language (HTML)</a> is the standard markup language for <strong>creating <u>web</u> pages</strong> and web applications.Web browsers receive HTML documents from a web server or from local storage and render them into multimedia web pages. HTML describes the structure of a web page semantically and originally included cues for the appearance of the document.
      <img src="coding.jpg" width="100%">
      </p><p style="margin-top:45px;">HTML elements are the building blocks of HTML pages. With HTML constructs, images and other objects, such as interactive forms, may be embedded into the rendered page. It provides a means to create structured documents by denoting structural semantics for text such as headings, paragraphs, lists, links, quotes and other items. HTML elements are delineated by tags, written using angle brackets.
      </p>
    </body>
    </html>
  `;
  response.end(template);
});
app.listen(3000);
```

코드를 살펴보자.

```js
var title = queryData.id;
```

- queryData는 query string을 객체 형식으로 저장한다. 
- queryData 객체의 id의 값을 title 변수에 저장한다.
  - URL의 query string에서 값 이름을 id로 사용하므로, title 변수의 값은 query string에서의 id의 값이다.
  - URL을 localhost:3000/?id=HTML 으로 사용하면 title의 값은 HTML이다.
- template 변수에 저장한 템플릿 리터럴에서 ${} 내부에 title 변수를 사용한다.

```js
if (_url == "/") {
  title = "Welcome";
}
```

- 루트(최상위 경로, localhost:3000)로 접속하면 _url이 "/"가 된다.
- 이 경우 title 변수에 "Welcome"을 저장한다.

```js
var template = `
  ...
  <ol>
    <li><a href="/?id=HTML">HTML</a></li>
    <li><a href="/?id=CSS">CSS</a></li>
    <li><a href="/?id=JavaScript">JavaScript</a></li>
  </ol>
  ...
`;
response.end(template);
```

- template 변수에 저장한 템플릿 리터럴을 웹페이지로 출력한다.
- 완성된 웹페이지를 출력하기 위해 html 코드를 template 변수에 저장하였다.
- a 태그의 href 속성 값에 query string을 넣었고, 링크에 해당하는 query string에 맞게 template이 적용된다.
- template 변수 내부에서 사용하는 title 변수가 query string에 따라 변경되므로 웹페이지가 동적으로 생성되어 출력된다.

