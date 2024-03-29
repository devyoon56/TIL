# WEB2 - Node.js

# Node.js로 웹서버 만들기

Node.js가 웹 서버 기능을 내장하고 있기 때문에 Node.js를 웹 서버로 사용할 수 있다.

Node.js를 웹 서버로 사용하는 코드

```js
var http = require("http");
var fs = require("fs");
var app = http.createServer(function (request, response) {
  var url = request.url;
  if (url == "/") {
    url = "/index.html";
  }
  if (url == "/favicon.ico") {
    response.writeHead(404);
    response.end();
    return;
  }
  response.writeHead(200);
  response.end(fs.readFileSync(__dirname + url));
});
app.listen(3000);
```

- 사용자에게 전송할 데이터를 생성하는 코드이다.
- 지금은 대략적으로만 이렇게 알고 넘어가자.

코드를 Node.js로 실행하는 방법

- main.js 자바스크립트 파일에 코드를 넣고 터미널에서 해당 파일을 Node.js로 실행시킨다.

```
node main.js
```

- 웹브라우저 주소창에 localhost:3000 을 입력하여 결과를 확인한다.

# 자바스크립트 문법 - 템플릿 리터럴

```js
var name = "egoing";
var letter = `Dear ${name} Lorem ipsum dolor sit amet, consectetur adipiscing elit. ...`;
console.log(letter);
```

- 템플릿 리터럴은 백틱(``)과 ${}를 사용한다.
- 백틱(``) 내부에 문자열을 입력하고, ${} 내부에 변수를 입력하면 변수의 값이 문자열로 치환된다.

# URL의 이해

URL 샘플

http://opentutorials.org:3000/main?id=HTML&page=12

  - `http`
    - protocol, 프로토콜, 통신 규칙으로 http를 사용한다.
    - 사용자가 서버에 접속할 때 어떤 방식으로 통신할 것인지를 나타낸다.
    - http는 웹브라우저와 웹서버가 서로 데이터를 주고 받기 위해 만들어진 통신 규칙이다.
  - `opentutorials.org`
    - host 또는 domain name
    - 인터넷에 연결된 특정 컴퓨터의 주소이다.
  - `3000`
    - 포트 번호
    - 한 대의 컴퓨터에 서버가 여러 개 있는 경우 클라이언트가 어떤 서버와 통신할지가 애매한 경우가 발생한다.
    - 클라이언트가 서버에 접속할 때 포트 번호를 명시하면 해당 포트번호에 연결된 서버와 통신한다.
  - `main`
    - path
    - 컴퓨터 안에 있는 어떤 디렉터리의 어떤 파일인지를 가리킨다.
  - `?id=HTML&page=12`
    - Query string
    - Query string을 사용해 클라이언트가 서버에게 정보를 전달한다.
    - `?id=HTML&page=12`는 id 값이 HTML이고 page 값이 12이라는 것을 나타낸다.
    - Query string은 물음표(?)로 시작하는 걸로 약속되어 있다.
    - 값과 값은 앰퍼센드(&)를 써서 구분하기로 약속되어 있다.
    - 값의 이름과 값은 =로 구분하기로 약속되어 있다.

# URL을 통해서 입력된 값 사용하기

http://localhost/?id=HTML

사용자가 이 URL을 사용하여 웹 애플리케이션에 접속했을 때 id 값이 무엇이냐에 따라 사용자에게 적당한 컨텐츠를 보여주려고 한다.

  - URL에서 id가 위치하는 부분(?id=HTML)이 query string이다.
  - Query string에 맞는 컨텐츠를 보여주려는 것이다.

Query string에 따라 다른 정보를 보여주려면 URL을 분석해서 query string을 추출해야 한다.

  - 키워드: nodejs url parse query string

main.js 코드

```js
var http = require("http");
var fs = require("fs");
var url = require("url");

var app = http.createServer(function (request, response) {
  var _url = request.url;

  // Query string을 추출하고 출력하기
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

nodejs로 웹 애플리케이션을 실행하고, 웹브라우저 주소창에 localhost:3000/?id=HTML을 입력한다.

코드 설명

- 결과를 확인하면 에러가 발생하지만, `queryData`가 객체인 것을 확인할 수 있다.
  - { id: 'HTML' }
  - queryData에는 query string이 객체 형식으로 들어온다는 것을 알 수 있다.
  - queryData.id 확인 결과 HTML인 것을 알 수 있다.
- `response.end(queryData.id)`
  - query string에 따라 다른 정보를 웹페이지에 출력한다.
  - id=HTML 이면 단순히 HTML이 출력된다.
  - id=CSS 이면 단순히 CSS가 출력된다.

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

코드 설명

```js
var queryData = url.parse(_url, true).query;
var title = queryData.id;
```

- queryData는 URL의 query string을 객체 형식으로 저장한다.
- queryData 객체의 id의 값을 title 변수에 저장한다.
  - URL의 query string에서 값 이름을 id로 사용하므로, title 변수의 값은 query string에서의 id의 값이다.
  - 예를 들어 URL을 localhost:3000/?id=HTML 으로 사용하면 title의 값은 query string인 id의 값 HTML이다.
- template 변수에 저장한 템플릿 리터럴에서 ${} 내부에 title 변수를 사용한다.

```js
if (_url == "/") {
  title = "Welcome";
}
```

- 루트, 즉 최상위 경로(URL이 단순히 localhost:3000인 경우)로 접속하면 _url이 "/"가 된다.
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
- a 태그의 href 속성 값에 query string을 넣었고, 각 a 태그에 해당하는 query string에 맞게 template이 적용된다.
- template 변수 내부에서 사용하는 title 변수가 query string에 따라 변경되므로 웹페이지가 동적으로 생성되어 출력된다.

# Node.js의 파일 읽기 기능

sample.txt 파일을 읽는 코드이다.

```js
var fs = require("fs");
fs.readFile("sample.txt", "utf8", function (err, data) {
  console.log(data);
});
```

- data를 출력하면 sample.txt 파일의 내용이 출력되는 것을 확인할 수 있다.

# App 제작 - 파일을 이용해 본문 구현

파일 내용을 읽어 웹페이지의 본문으로 출력하려고 한다.

파일 내용을 읽어 웹페이지의 본문으로 출력하는 main.js 코드

```js
fs.readFile(`data/${queryData.id}`, "utf8", function (err, description) {
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
      <p>${description}</p>
    </body>
    </html>
  `;
  response.end(template);
});
```

- Node.js의 파일 읽기 기능을 사용한다.
- readFile 메서드의 첫 번째 인자: `data/${queryData.id}`
  - 첫 번째 인자로 읽을 파일의 경로를 전달한다.
  - data 폴더 내부에 저장한 파일을 사용한다.
  - query string 객체의 id 값이 HTML, CSS, JavaScript이다.
  - data 폴더 내부에 저장한 파일 이름도 HTML, CSS, JavaScript이다.
- query string에 따라 data 폴더에 저장한 파일의 내용을 읽으면, 세 번째 인자로 전달한 함수의 매개변수 description에 전달된다.
- 세 번째 인자로 전달한 함수가 실행된다.
  - template 변수에서 ${} 내부에 description 매개변수를 사용해 본문을 완성하고 웹페이지를 출력한다.

# App 제작 - Not found 구현

1. 사용자가 query string이 없는 루트로 들어오는 경우 홈페이지를 출력하려고 한다.
2. 웹앱이 지원하는 query string을 사용하지 않는 URL로 사용자가 접속하는 경우 파일을 찾을 수 없다는 오류 메시지를 사용자에게 전송하려고 한다.

먼저 사용자가 루트로 접속하는지 여부를 파악해야 한다. 사용자가 루트로 접속하는 경우는 URL에 path 정보가 붙지 않는 것을 말한다.

- 예를 들어 localhost:3000 과 같은 경우를 말한다.

main.js 코드

```js
var http = require("http");
var fs = require("fs");
var url = require("url");

var app = http.createServer(function (request, response) {
  var _url = request.url;
  var queryData = url.parse(_url, true).query;
  var title = queryData.id;

  console.log(url.parse(_url, true));

  fs.readFile(`data/${queryData.id}`, "utf8", function (err, description) {
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
        <p>${description}</p>
      </body>
      </html>
    `;
    response.writeHead(200);
    response.end(template);
  });
});
app.listen(3000);
```

URL 분석 결과를 확인한다.

```js
console.log(url.parse(_url, true));
```

확인 결과

`
Url {
  protocol: null,
  slashes: null,
  auth: null,
  host: null,
  port: null,
  hostname: null,
  hash: null,
  search: '?id=HTML',
  query: [Object: null prototype] { id: 'HTML' },
  pathname: '/',
  path: '/?id=HTML',
  href: '/?id=HTML'
}
`

- path는 query string을 포함한다.
- pathname은 query string이 URL에 있다고 하더라도 query string을 제외한 path만 보여준다.

pathname을 추출하고 pathname으로 사용자의 루트 접속 여부를 확인한다.

```js
...
var pathname = url.parse(_url, true).pathname;
...

if (pathname === "/") {
  // 사용자가 루트로 접속한 경우와
  // 웹앱이 지원하는 query string을 사용해서 접속한 경우
  // 웹페이지를 완성해서 표시
  fs.readFile(`data/${queryData.id}`, "utf8", function (err, description) {
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
        <p>${description}</p>
      </body>
      </html>
    `;
    response.writeHead(200);
    response.end(template);
  });
} else {
  // 사용자가 루트로 접속하지 않은 경우와
  // 웹앱이 지원하지 않는 경로로 접속한 경우
  // 에러를 표시
  response.writeHead(404);
  response.end("Not found");
}
```

웹브라우저가 웹서버에 접속했을 때 웹서버는 이에 응답한다. 이때 웹브라우저와 웹서버 사이의 접속에 문제가 없는지, 에러가 있는지 등에 대한 중요한 정보를 기계와 기계가 서로 통신하기 위한 간결한 약속이 필요하다.

- `response.writeHead(200)`
  - `200`이라는 약속된 숫자를 서버가 브라우저에게 전달하면 파일을 성공적으로 전송했다라는 의미이다.
- `response.writeHead(404)`
  - 파일을 찾을 수 없는 경우 `404`라는 약속된 숫자를 서버가 브라우저에게 전달한다.

# App 제작 - 홈페이지 구현

사용자가 루트로 접속하는 경우 표시할 홈페이지를 아직 완성하지 않았다.

```js
...
var queryData = url.parse(_url, true).query;
console.log(queryData);
...
```

- 루트로 접속해서 queryData를 확인한다.
- 루트로 접속하는 경우 query string을 저장하는 `queryData`에는 아무것도 저장되지 않는다.
  - `[Object: null prototype] {}`

```js
if (pathname === "/") {
    if (queryData.id === undefined) {
      // 사용자가 루트로 접속한 경우 웹페이지를 완성해서 표시
      // ...
    } else {
      // 웹앱이 지원하는 query string을 사용해서 접속한 경우 웹페이지를 완성해서 표시
      // ...
    }
  } else {
    // 사용자가 루트로 접속하지 않은 경우와
    // 웹앱이 지원하지 않는 경로로 접속한 경우
    // 에러를 표시
    response.writeHead(404);
    response.end("Not found");
  }
```

- `queryData`에 아무것도 저장되지 않는 경우 `id` 값을 가져오면 `undefined`를 얻는다.
- 이것을 확인해서 사용자가 루트로 접속한 경우 홈페이지를 완성해서 표시한다.
- 또한 웹앱이 지원하는 query string을 사용해서 접속한 경우 웹페이지를 완성해서 표시한다.

# Node.js에서 파일 목록 알아내기

```js
// 코드 실행 위치 기준으로 테스트폴더 경로 작성
var testFolder = "./data";
var fs = require("fs");

fs.readdir(testFolder, function (error, filelist) {
  console.log(filelist);
});
```

실행 결과

- `[ 'CSS', 'HTML', 'JavaScript' ]`
- 폴더 내부에 존재하는 파일들의 이름을 배열 형태로 반환하는데, 두 번째 인자로 전달한 함수의 filelist 매개변수에 대입된다.

# App 제작 - 글목록 출력하기

data 폴더에 파일을 추가하거나 삭제해도 웹페이지에서 그 변경사항이 ul, li 태그에 자동으로 반영되지 않는 문제점이 있다.

파일 목록을 읽어서 ul, li 태그를 동적으로 생성하고 글목록을 출력할 수 있다.

```js
fs.readdir("./data", function (err, filelist) {
  var title = "Welcome";
  var description = "Hello, Node.js";
  var list = "<ul>";
  var i = 0;
  while (i < filelist.length) {
    list =
      list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
    i += 1;
  }
  list = list + "</ul>";

  var template = `
    <!doctype html>
    <html>
    <head>
      <title>WEB1 - ${title}</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1>
      ${list}
      <h2>${title}</h2>
      <p>${description}</p>
    </body>
    </html>
  `;
  response.writeHead(200);
  response.end(template);
});
```

- `list` 변수에 여는 ul 태그를 추가한다.
- 파일 목록과 반복문을 이용하여 li 태그를 추가한다.
  - Query string id의 값과 a 태그의 컨텐츠로 `filelist`의 값을 사용한다.
  - 글목록을 data 폴더의 파일 목록에 맞게 동적으로 생성한다.
- 마지막으로 닫는 ul 태그를 추가한다.
- `list` 변수를 웹페이지에서 글목록을 출력하고자 하는 곳에 배치한다.

이제 data 폴더에 파일을 추가하고 파일 내용을 작성하면, 추가한 파일에 대한 글목록이 웹페이지에 자동으로 추가되고 파일 내용이 본문으로 출력된다.

# App 제작 - 함수를 이용해서 정리정돈하기

함수를 이용해서 코드를 정리정돈한다.

완성된 웹페이지를 출력하기 위한 템플릿 코드를 반환하는 함수

```js
function templateHTML(title, list, body) {
  return `
    <!doctype html>
    <html>
    <head>
      <title>WEB1 - ${title}</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1>
      ${list}
      ${body}
    </body>
    </html>
  `;
}
```

파일 목록을 사용하여 ul, li 태그를 동적으로 생성하는 함수

```js
function templateList(filelist) {
  var list = "<ul>";
  var i = 0;
  while (i < filelist.length) {
    list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
    i += 1;
  }
  list = list + "</ul>";

  return list;
}
```

템플릿과 리스트를 사용하고 싶은 곳에서 호출한다.

```js
if (pathname === "/") {
  if (queryData.id === undefined) {
    // 사용자가 루트로 접속한 경우 웹페이지를 완성해서 표시
    fs.readdir("./data", function (err, filelist) {
      var title = "Welcome";
      var description = "Hello, Node.js";
      var list = templateList(filelist);
      var template = templateHTML(
        title,
        list,
        `<h2>${title}</h2>${description}`
      );
      response.writeHead(200);
      response.end(template);
    });
  } else {
    // 웹앱이 지원하는 query string을 사용해서 접속한 경우 웹페이지를 완성해서 표시
    fs.readdir("./data", function (err, filelist) {
      fs.readFile(
        `data/${queryData.id}`,
        "utf8",
        function (err, description) {
          var title = queryData.id;
          var list = templateList(filelist);
          var template = templateHTML(
            title,
            list,
            `<h2>${title}</h2>${description}`
          );
          response.writeHead(200);
          response.end(template);
        }
      );
    });
  }
}
```

- 코드 중복이 제거되었다.
- 코드 가독성이 좋아졌다.

# Node.js에서 동기와 비동기1

현실에서 어떤 작업을 한다고 생각해 보자.

동기synchronous적으로 일을 처리하기

- 작업 A를 시작한다.
- 작업 A를 끝내고 작업 B를 시작한다.
- 작업 B를 끝내고 작업 C를 시작한다.
- 직렬적인 처리 방식

비동기asynchronous적으로 일을 처리하기

- 작업 A를 시작한다.
- 작업 A를 누군가에게 넘기고 작업 A를 종료하면 나에게 알려줄 것을 말한다.
- 곧바로 작업 B를 시작한다.
- 현재 작업 A와 작업 B는 동시에 진행 중이다.
- 병렬적인 처리 방식

Node.js는 비동기적으로 일을 처리하기 위한 도구를 가지고 있다.

# Node.js에서 동기와 비동기2

동기와 비동기가 코드 레벨에서 어떤 차이가 있는지 알아 보자.

파일 내용을 읽어 출력하는 동기 코드(`readFileSync`)

```js
var fs = require("fs");
console.log("A");
var result = fs.readFileSync("syntax/sample.txt", "utf8");
console.log(result);
console.log("C");
```

```
// 실행 결과
A
B
C
```

- sample.txt의 파일 내용은 B이다.
- 코드 실행 결과 A, B, C가 출력된다.
- `readFileSync` 메서드
  - 첫 번째 인자로 전달한 파일 경로에서 파일 내용을 읽는다.
  - 파일 내용을 반환한다.
- `readFileSync` 메서드 실행 결과를 `result` 변수에 대입한다.
- 코드를 작성한 순서대로 결과가 출력되는 것을 알 수 있다.

파일 내용을 읽어 출력하는 비동기 코드(`readFile`)

```js
var fs = require("fs");
console.log("A");
fs.readFile("syntax/sample.txt", "utf8", function (err, result) {
  console.log(result);
});
console.log("C");
```

```
// 실행 결과
A
C
B
```

- 코드 실행 결과 A, C, B가 출력된다.
- 코드를 작성한 순서대로 결과가 출력되지 않는다.
- `readFile` 메서드
  - 첫 번째 인자로 전달한 파일 경로에서 파일 내용을 읽는다.
  - 파일 내용을 모두 읽으면, 세 번째 인자로 전달한 함수의 두 번째 인자 `result`에 읽은 파일 내용을 전달하면서, 세 번째 인자로 전달한 함수를 실행한다.
  - 세 번째 인자로 전달한 함수 실행 결과로 B가 출력된다.
- `readFile` 메서드는 비동기로 실행되므로 메서드의 실행 결과를 기다리지 않고 곧바로 아래 코드를 실행한다.
- 따라서 C가 먼저 출력되고, `readFile` 메서드가 실행을 마치면 세 번째 인자로 전달한 함수가 실행되면서 B가 출력된다.

# JavaScript - Callback

'A'를 출력하는 간단한 함수 a이다.

```js
function a() {
  console.log('A');
}
a();
```

함수 a와 같지만 형식이 다른 코드가 있다.

```js
var a = function () {
  console.log('A');
};
a();
```

- 이 코드는 변수 a의 값으로서 함수를 정의한다.
- 이것은 **자바스크립트에서 함수는 값이다**라는 것을 의미한다.

실행 시간이 오래 걸리는 `slowfunc`라는 함수가 있다.

```js
var a = function () {
  console.log('A');
};

function slowfunc(callback) {
  // ...
  callback();
}

slowfunc(a);
```

- `slowfunc` 함수를 모두 실행한 뒤에 어떤 함수를 실행하기 위해 인자로 콜백을 받는다.
  - 인자로 전달받은 콜백을 마지막에 실행한다.
- `slowfunc` 함수를 실행하면서 `변수 a`를 전달한다.
  - `callback` 매개변수는 `변수 a`가 가리키는 함수를 가리킨다.
  - `slowfunc` 함수 내부에서 `callback`을 호출하면 `변수 a`가 가리키는 함수가 호출된다.

# Node.js의 패키지 매니저와 PM2

패키지

- 소프트웨어를 부르는 여러 표현들 중의 하나이다.
- 독립적으로 실행되는 프로그램도 패키지라고 할 수 있다.
- 어떤 프로그램 안에서 부품으로 사용되는 작은 프로그램도 패키지라고 할 수 있다.

패키지 매니저

- 패키지를 관리(생성, 설치, 업데이트, 삭제)하는 프로그램이다.

NPM

- Node.js에서 가장 광범위하게 사용되는 패키지 매니저
- Node.js로 만들어진 프로그램들을 쉽게 설치할 수 있게 도와줌

PM2

- 실행 중인 프로세스가 예기치 못하게 종료될 수 있다.
  - PM2는 프로세스를 감시하다가 프로세스가 종료되면 다시 실행해주는 역할을 한다.
- 프로그램을 수정하면 Node.js를 종료하고 다시 실행해야 변경사항이 반영되었다.
  - PM2는 프로그램이 수정되는지를 감시하다가 수정되면 자동으로 프로그램을 껐다가 다시 실행시켜서 수동으로 종료하고 다시 실행해야 하는 불편함을 제거해준다.

npm으로 PM2를 설치하기

```
npm install pm2 -g
```

PM2로 main.js 실행하기

```
pm2 start main.js
```

PM2로 실행 중인 프로그램 확인하기(별도 창에서)

```
pm2 monit
```

PM2로 실행 중인 프로세스의 리스트 확인하기

```
pm2 list
```

PM2로 실행 중인 프로세스 종료하기

```
pm2 stop main
```

- main: 프로세스 리스트로 확인한 프로세스의 이름

프로그램 변경사항을 감시하고 변경사항이 있으면 자동으로 프로그램 다시 시작하기

```
pm2 start main.js --watch
```

프로그램에 발생한 에러와 프로그램 변경사항을 저장했다는 것을 화면에 출력하기

```
pm2 log
```

# HTML form

사용자가 웹을 통해 컨텐츠를 생성하고 수정하고 삭제하기 위해 서버로 데이터를 전송하는 방식인 **HTML form**이 있다.

```html
<form action="http://localhost:3000/create_process">
  <p><input type="text" name="title" /></p>
  <p>
    <textarea name="description"></textarea>
  </p>
  <p>
    <input type="submit" />
  </p>
</form>
```

- `form` 태그는 form 태그 안에 있는 각각의 컨트롤들에 사용자가 입력한 정보를 submit 버튼을 눌렀을 때, form 태그의 action 속성이 가리키는 서버로 query string의 형태로 데이터를 전송하는 HTML의 기능이다.
- name 속성이 `title`인 input 태그와 name 속성이 `description`인 textarea 태그에 어떤 값을 입력하고 submit 버튼을 클릭했을 때
  - URL은 `http://localhost:3000/create_process?title=hi&description=lorem` 인 것을 확인할 수 있다.
  - 이런 URL은 좋지 않다.
  - 데이터를 전송할 때 주소에 데이터가 포함되어 있다면, 해당 주소를 누군가에게 복사해서 전달했을 때, 그 사람이 전달받은 주소를 클릭해서 들어오면 서버에 있는 정보가 수정되거나 삭제되거나 생성될 수 있다.
  - 서버에서 데이터를 가져올 때는 query string을 사용한다.
  - 서버에 데이터를 생성, 수정, 삭제하는 것과 같은 행위를 할 때는 필요한 데이터를 URL로 보내는 것은 절대 안됀다.

서버에 데이터를 생성, 수정, 삭제하는 것과 같은 행위를 할 때는 form 태그의 `method` 속성을 사용한다.

```html
<form action="http://localhost:3000/create_process" method="post">
  <p><input type="text" name="title" /></p>
  <p>
    <textarea name="description"></textarea>
  </p>
  <p>
    <input type="submit" />
  </p>
</form>
```

- input 태그와 textarea 태그에 값을 입력하고 submit 버튼을 클릭했을 떄
  - URL은 `http://localhost:3000/create_process` 인 것을 확인할 수 있다.
  - Query string은 보이지 않는데, 서버로 은밀하게 전송하기 때문이다.

# App 제작 - 글생성 UI 만들기

글목록 밑에 글을 생성하는 페이지로 이동하는 링크를 추가한다.

```js
function templateHTML(title, list, body) {
  return `
    <!doctype html>
    <html>
    <head>
      <title>WEB2 - ${title}</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1>
      ${list}
      <a href="/create">create</a>
      ${body}
    </body>
    </html>
  `;
}
```

- 추가한 a 태그의 href 속성 값이 `/create`이다.
- 추가한 a 태그를 클릭했을 때 URL은 `http://localhost:3000/create` 이다.

추가한 a 태그를 클릭했을 때 URL 분석 결과를 확인하면 다음과 같다.

`
Url {
protocol: null,
slashes: null,
auth: null,
host: null,
port: null,
hostname: null,
hash: null,
search: null,
query: [Object: null prototype] {},
pathname: '/create',
path: '/create',
href: '/create'
}
`

- `pathname`을 이용하여 글생성 페이지로 이동했다는 것을 확인할 수 있다.

사용자가 글생성 페이지로 이동한 경우 웹페이지를 완성해서 표시하는 코드를 추가한다.

```js
if (pathname === "/") {
  ...
} else if (pathname === "/create") {
  // 사용자가 글생성 페이지로 이동한 경우 웹페이지를 완성해서 표시
  fs.readdir("./data", function (err, filelist) {
    var title = "WEB - create";
    var list = templateList(filelist);
    var template = templateHTML(
      title,
      list,
      `<form action="http://localhost:3000/create_process" method="post">
        <p><input type="text" name="title" placeholder="title"/></p>
        <p>
          <textarea name="description" placeholder="description"></textarea>
        </p>
        <p>
          <input type="submit" />
        </p>
      </form>`
    );
    response.writeHead(200);
    response.end(template);
  });
} else {
  ...
}
```

글생성 페이지에서 입력한 값이 서버로 전송되는 것을 확인하기(개발자 도구)

- input 태그와 textarea 태그에 값을 입력하고 submit 버튼을 클릭
- Network 메뉴에서 create_process 항목 클릭
- Payload 메뉴 클릭
  - title: (input 태그에 입력한 값)
  - description: (textarea 태그에 입력한 값)

# App 제작 - POST 방식으로 전송된 데이터 받기

form 태그에서 post 방식으로 전송한 데이터를 가져와야 한다.

form 태그의 action 속성 값에서 사용한 URL에서 pathname을 이용한다.

```js
if (pathname === "/") {
  ...
} else if (pathname === "/create") {
  // 사용자가 글생성 페이지로 이동한 경우 웹페이지를 완성해서 표시
  ...
} else if (pathname === "/create_process") {
  var body = "";
  request.on("data", function (data) {
    body = body + data;
  });
  request.on("end", function () {
    var post = qs.parse(body);
    var title = post.title;
    var description = post.description;
    console.log(post);
  });
  response.writeHead(200);
  response.end("Success!");
} else {
  ...
}
```

웹브라우저가 post 방식으로 데이터를 전송할 때 데이터가 많으면 프로그램이 종료되는 등의 문제가 발생한다. Node.js에서는 post 방식으로 전송되는 데이터가 많을 때 다음과 같은 처리 방법을 제공한다.

```js
var body = "";
request.on("data", function (data) {
  body = body + data;
});
```

- 총 데이터의 조각들을 수신하고, 데이터 조각을 수신할 때마다 서버는 콜백 함수를 호출하도록 약속되어 있다.
- 그리고 콜백 함수를 호출할 때 data 매개변수를 통해 수신한 데이터를 인자로 넘긴다.
- `body = body + data`
  - body 변수에 수신한 데이터를 추가한다.

데이터 조각들을 수신하다가 더이상 수신할 데이터가 없으면 "end" 다음의 콜백 함수를 호출하도록 약속되어 있다. "end" 다음의 콜백 함수가 호출된다면 데이터 수신이 끝났다라고 생각할 수 있다.

```js
var qs = require("querystring");
...
request.on("end", function () {
  var post = qs.parse(body);
  var title = post.title;
  var description = post.description;
  console.log(post);
});
```

- `querystring` 모듈의 `parse` 함수를 사용해서 수신한 데이터를 객체화할 수 있다.
  - form 태그를 통해 전송한 데이터를 개발자 도구에서 확인하면 다음과 같다.
    - title: (input 태그에 입력한 값)
    - description: (textarea 태그에 입력한 값)
  - 이 데이터가 객체화되어 `post` 변수에 저장된다.
  - `title`, `description` 변수에 각각 저장한다.

# App 제작 - 파일생성과 리다이렉션

POST 방식으로 전송한 데이터를 data 디렉터리 안에 파일 형태로 저장하는 방법에 대해 알아보자.

```js
request.on("end", function () {
  var post = qs.parse(body);
  var title = post.title;
  var description = post.description;

  fs.writeFile(`data/${title}`, description, "utf8", function (err) {
    response.writeHead(200);
    response.end("Success!");
  });
});
```

- `File system` 모듈의 `writeFile` 함수를 사용한다.
- data 디렉터리 안에 파일을 저장한다.
  - 파일이름: `title`
  - 파일내용: `description`
- 파일 저장 작업이 끝나면 네 번째 인자로 전달한 콜백 함수가 실행되면서 Success! 메시지가 웹페이지에 출력된다.

파일로 저장하고 나면 웹페이지에 단순히 Success! 라는 메시지만 출력되는데, 사용자 입장에서 당황스러울 수 있다. 따라서, 사용자를 사용자가 생성한 파일을 볼 수 있는 웹페이지로 이동시키려고 한다.

- 이것을 `리다이렉션`이라고 한다.
- `리다이렉션`은 사용자가 어떤 페이지에 접속했을 때 내부 처리 과정을 통해 다른 페이지로 튕겨내는 것을 말한다.

```js
request.on("end", function () {
  var post = qs.parse(body);
  var title = post.title;
  var description = post.description;

  fs.writeFile(`data/${title}`, description, "utf8", function (err) {
    response.writeHead(302, { Location: `/?id=${title}` });
    response.end();
  });
});
```

- `response.writeHead(302, ...);`
  - 302: 페이지를 리다이렉션한다.

# App 제작 - 글수정: 수정 링크 생성

글을 수정할 수 있는 링크를 생성한다. 먼저 HTML 템플릿을 반환하는 `templateHTML` 함수를 수정한다.

```js
function templateHTML(title, list, body, control) {
  return `
    <!doctype html>
    <html>
    <head>
      <title>WEB2 - ${title}</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1>
      ${list}
      ${control}
      ${body}
    </body>
    </html>
  `;
}
```

- 기존의 a 태그가 위치하던 부분을 control 매개변수와 ${}를 사용하여 교체하였다.

모든 웹페이지에서 글수정 링크를 보여주는 것이 아니라 query string을 주소에 포함하는 웹페이지에 대해서만 글수정 링크를 보여주려고 한다.

```js
if (pathname === "/") {
  if (queryData.id === undefined) {
    // 사용자가 루트로 접속한 경우 웹페이지를 완성해서 표시
    fs.readdir("./data", function (err, filelist) {
      var title = "Welcome";
      var description = "Hello, Node.js";
      var list = templateList(filelist);
      var template = templateHTML(
        title,
        list,
        `<h2>${title}</h2>${description}`,
        `<a href="/create">create</a>`
      );
      response.writeHead(200);
      response.end(template);
    });
  } else {
    // 웹앱이 지원하는 query string을 사용해서 접속한 경우 웹페이지를 완성해서 표시
    fs.readdir("./data", function (err, filelist) {
      fs.readFile(
        `data/${queryData.id}`,
        "utf8",
        function (err, description) {
          var title = queryData.id;
          var list = templateList(filelist);
          var template = templateHTML(
            title,
            list,
            `<h2>${title}</h2>${description}`,
            `<a href="/create">create</a> <a href="/update?id=${title}">update</a>`
          );
          response.writeHead(200);
          response.end(template);
        }
      );
    });
  }
}
```

- 루트로 접속한 경우에는 글생성 링크만 추가한다.
- Query string을 포함하는 웹페이지에 접속한 경우에는 글생성 링크 뿐만 아니라 글수정 링크까지 추가한다.
  - templateHTML 함수 호출 시 전달하는 네 번째 인자에서 차이가 있다.
  - 글수정 링크: `<a href="/update?id=${title}">update</a>`
    - pathname을 /update로, query string의 경우 id에 대한 값을 title로 설정하였다.

# App 제작 - 글수정: 수정할 정보 전송

글수정 링크를 클릭했을 때 보여질 화면을 만들 차례다. 이 화면을 만들기 위해 두 가지가 필요하다.

1. form 태그
2. 수정하고자 하는 데이터를 form에 미리 넣어두어야 함

```js
else if (pathname === "/update") {
  fs.readdir("./data", function (err, filelist) {
    fs.readFile(`data/${queryData.id}`, "utf8", function (err, description) {
      var title = queryData.id;
      var list = templateList(filelist);
      var template = templateHTML(
        title,
        list,
        `<form action="/update_process" method="post">
          <input type="hidden" name="id" value="${title}">
          <p>
            <input type="text" name="title" placeholder="title" value="${title}"/>
          </p>
          <p>
            <textarea name="description" placeholder="description">${description}</textarea>
          </p>
          <p>
            <input type="submit" />
          </p>
        </form>`,
        `<a href="/create">create</a> <a href="/update?id=${title}">update</a>`
      );
      response.writeHead(200);
      response.end(template);
    });
  });
}
```

글수정 링크를 클릭했을 때 이동할 웹페이지를 생성한다.

- form의 action 속성 값은 `/update_process`이다.
- `<input type="hidden" name="id" value="${title}">`
  - 사용자가 제목을 수정할 경우 제목에 맞는 파일을 디렉터리에서 찾을 수 없다.
  - 이런 경우 사용자가 수정하는 정보와 우리가 수정하고자 하는 파일을 구분해서 전송해야 한다.
  - 사용자에게 이 input 태그를 보여주지 않기 위해 hidden 타입으로 설정하였다.
- input 태그의 value 속성과 textarea 태그의 컨텐츠에 수정하고자 하는 데이터를 미리 넣어둔다.

# App 제작 - 글수정: 파일명 변경, 내용 저장

```js
else if (pathname === "/update_process") {
  var body = "";
  request.on("data", function (data) {
    body = body + data;
  });
  request.on("end", function () {
    var post = qs.parse(body);
    var id = post.id;
    var title = post.title;
    var description = post.description;
    console.log(post);

    // 파일명 변경
    fs.rename(`data/${id}`, `data/${title}`, function (error) {
      // 내용 변경
      fs.writeFile(`data/${title}`, description, "utf8", function (err) {
        response.writeHead(302, { Location: `/?id=${title}` });
        response.end();
      });
    });
  });
}
```

- 파일명을 변경하기 위해 File system의 `rename` 함수를 사용한다.
  - 첫 번째 인자로 현재 파일 경로를 전달한다. 현재 파일 경로를 전달하기 위해 id 값을 사용하였다. 이 값은 name 속성 값이 id인 input 태그의 value 속성 값이다.
  - 두 번째 인자로 새로운 파일 경로를 전달한다.
  - 파일명을 변경하면 세 번째 인자인 콜백 함수가 실행된다.
- 파일명 변경 후 내용을 변경하고 변경한 내용으로 업데이트된 웹페이지로 리다이렉션한다.

# App 제작 - 글삭제: 삭제 버튼 구현

삭제 버튼의 경우, 글목록에서 글을 선택한 상태에서 삭제 버튼이 활성화된다.

```js
fs.readdir("./data", function (err, filelist) {
  fs.readFile(
    `data/${queryData.id}`,
    "utf8",
    function (err, description) {
      var title = queryData.id;
      var list = templateList(filelist);
      var template = templateHTML(
        title,
        list,
        `<h2>${title}</h2>${description}`,
        `<a href="/create">create</a>
        <a href="/update?id=${title}">update</a>
        <form action="/delete_process" method="post">
          <input type="hidden" name="id" value="${title}">
          <input type="submit" value="delete">
        </form>`
      );
      response.writeHead(200);
      response.end(template);
    }
  );
});
```

- 삭제 버튼을 구현하기 위해 form 태그를 사용한다.
  - 삭제 기능을 구현할 때 query string을 사용하는 get 방식은 절대 사용해선 안됀다.
  - action 속성 값은 /delete_process로, method 속성 값은 post로 설정하였다.
- input 태그의 type 속성을 submit으로, value 속성을 delete로 설정하여 삭제 버튼을 구현하였다.

# App 제작 - 글삭제 기능 완성

```js
else if (pathname === "/delete_process") {
  var body = "";
  request.on("data", function (data) {
    body = body + data;
  });
  request.on("end", function () {
    var post = qs.parse(body);
    var id = post.id;

    // 파일 삭제
    fs.unlink(`data/${id}`, function (err) {
      // 파일 삭제 후 홈페이지로 리다이렉션
      response.writeHead(302, { Location: `/` });
      response.end();
    });
  });
}
```

- id 변수의 값은 글제목이고 이것은 파일 이름과 같다.
- File system 모듈의 unlink 함수를 사용해서 파일을 삭제한다.
  - 첫 번째 인자로 삭제할 파일 경로를 전달한다.
  - 두 번째 인자로 파일 삭제 후 실행할 콜백 함수를 전달한다.
- 파일 삭제 후 홈페이지로 리다이렉션한다.

# App 제작 - 템플릿 기능 정리정돈하기

기존의 템플릿 기능은 다음과 같다.

```js
function templateHTML (title, list, body, control) {
  return `
    <!doctype html>
    <html>
    <head>
      <title>WEB2 - ${title}</title>
      <meta charset="utf-8">
    </head>
    <body>
      <h1><a href="/">WEB</a></h1>
      ${list}
      ${control}
      ${body}
    </body>
    </html>
  `;
}

function templateList (filelist) {
  var list = "<ul>";
  var i = 0;
  while (i < filelist.length) {
    list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
    i += 1;
  }
  list = list + "</ul>";

  return list;
}
```

이 두 함수를 `template`이라는 객체의 프로퍼티(메서드)로 재구성한다.

```js
var template = {
  HTML: function (title, list, body, control) {
    return `
      <!doctype html>
      <html>
      <head>
        <title>WEB2 - ${title}</title>
        <meta charset="utf-8">
      </head>
      <body>
        <h1><a href="/">WEB</a></h1>
        ${list}
        ${control}
        ${body}
      </body>
      </html>
    `;
  },
  list: function (filelist) {
    var list = "<ul>";
    var i = 0;
    while (i < filelist.length) {
      list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
      i += 1;
    }
    list = list + "</ul>";

    return list;
  },
};
```

마지막으로, 이전에 `templateHTML`, `templateList` 함수를 사용했던 모든 코드를 `template` 객체의 메서드를 사용하도록 수정한다.

# Node.js 모듈의 형식

모듈은 객체를 정리정돈할 수 있는 더 큰 틀의 정리정돈 도구이다.

mpart.js 코드

```js
var M = {
  v: "v",
  f: function () {
    console.log(this.v);
  },
};

module.exports = M;
```

- `module.exports = M`
  - mpart.js 파일에서 변수 M이 가리키는 객체를 모듈 바깥에서 사용할 수 있도록 export한다는 의미라고 이해하자.

muse.js 코드

```js
var part = require("./mpart.js");
console.log(part);  // { v: 'v', f: [Function: f] }

part.f();  // v
```

- 모듈을 가져오기 위해 require를 사용한다.
- mpart.js 파일에서 export한 객체를 가져온다.

# App 제작 - 모듈의 활용

템플릿 기능을 객체화한 `template` 객체를 모듈화한다.

lib 디렉터리를 만들고, 디렉터리 내부에 template.js 파일을 생성한다.

```js
module.exports = {
  HTML: function (title, list, body, control) {
    return `
      <!doctype html>
      <html>
      <head>
        <title>WEB2 - ${title}</title>
        <meta charset="utf-8">
      </head>
      <body>
        <h1><a href="/">WEB</a></h1>
        ${list}
        ${control}
        ${body}
      </body>
      </html>
    `;
  },
  list: function (filelist) {
    var list = "<ul>";
    var i = 0;
    while (i < filelist.length) {
      list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
      i += 1;
    }
    list = list + "</ul>";

    return list;
  },
};
```

- template 객체 코드를 넣는다.
- module.exports를 사용하여 객체를 모듈 바깥에서 사용할 수 있도록 export한다.

main.js 코드

```js
var template = require("./lib/template.js");
```

- lib 디렉터리의 template.js 모듈에서 export한 객체를 `template` 변수에 저장한다.
- 이전에 템플릿 기능을 사용했던 것처럼 template 변수가 가리키는 객체의 `HTML`, `list` 메서드를 사용한다.

# App 제작 - 입력정보에 대한 보안

데이터베이스 관리자 아이디와 비밀번호를 저장하는 password.js 파일이 있다.

```js
module.exports = {
  id: "egoing",
  password: "111111",
};
```

사용자가 `localhost:3000/?id=../password.js` 주소로 접속하는 경우 그대로 password.js 파일 내용이 웹페이지에 출력된다.

이런 보안 문제점들을 해결하기 위해 Nodejs의 `path` 모듈을 사용한다.

```js
var path = require("path");
```

사용자로부터 경로가 입력되는 모든 곳에 대해 코드를 수정해야 한다.

```js
var filteredId = path.parse(queryData.id).base;
fs.readFile(`data/${filteredId}`, "utf8", function (err, description) {
  ...
});
```

```js
request.on("end", function () {
  var post = qs.parse(body);
  var id = post.id;
  var filteredId = path.parse(id).base;
  // 파일 삭제
  fs.unlink(`data/${filteredId}`, function (err) {
    // 파일 삭제 후 홈페이지로 리다이렉션
    response.writeHead(302, { Location: `/` });
    response.end();
  });
});
```

# App 제작 - 출력정보에 대한 보안(1)

오염된 정보가 출력될 때 보안 이슈가 발생할 수 있다.

공격자가 글 내용으로 악의적인 자바스크립트 코드를 입력할 수 있다.

```html
<script>
  location.href = "http://...";
</script>
```

- 사용자가 이 글을 클릭하면 해당 주소로 이동된다.

이것 말고도 사용자의 로그인 정보를 갈취하는 등의 자바스크립트 코드를 심어놓을 수 있다. 따라서 사용자가 입력한 정보를 출력하는 경우 문제가 될 수 있는 것들을 필터링하는 작업을 해야 한다.

간단하지만 수동적인 방법이 있다. script 태그를 태그로 해석하지 않도록 <>를 그대로 웹브라우저에 출력하는 것이다. (HTML Entities)

```html
&lt;script&gt;
  location.href = "http://...";
&lt;/script&gt;
```

- 사용자가 이 글을 클릭하면 해당 코드가 그대로 웹브라우저에 출력된다.

# App 제작 - 출력정보에 대한 보안(2)

```
npm init
```

- npm init 으로 패키지를 생성한다.

```
npm install -S sanitize-html
```

- 사용자가 입력한 정보를 출력할 때 문제가 될 수 있는 것들을 필터링해주는 외부 패키지인 `sanitize-html`을 설치한다.
- `-S` 옵션으로 진행할 프로젝트에서만 사용할 패키지로서 설치한다.

# App 제작 - 출력정보에 대한 보안(3)

`sanitize-html` 모듈을 사용한다.

```js
var sanitizeHtml = require("sanitize-html");
```

```js
var sanitizedTitle = sanitizeHtml(title);
var sanitizedDescription = sanitizeHtml(description);
```

- sanitizeHtml 함수에 필터링할 값을 넣으면 필터링된 값이 반환된다.
- script 태그가 전달되면 script 태그와 그 콘텐츠는 아예 삭제된다.
- 옵션으로 예외를 둘 수도 있다. (sanitize-html 사용법 참고)

# API와 CreateServer

API

- Application Programming Interface의 약자
- Node.js로 구현한 웹애플리케이션은 Node.js가 가지고 있는 기능을 호출해서 동작한다.
- fs.readFile 함수 사용법은 Node.js 개발자들이 제공한다.
- fs.readFile 함수는 Node.js 개발자들과 이 함수를 사용하는 개발자들의 약속된 조작 장치이다.
- 이런 조작 장치를 Interface라고 한다.
- 우리는 이런 Interface를 사용하여 Application을 Programming한다.