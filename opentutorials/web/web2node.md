# WEB2 - Node.js

# Node.js로 웹서버 만들기

Node.js가 웹 서버 기능을 내장하고 있기 때문에 Node.js를 웹 서버로 사용할 수 있다.

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

- 사용자에게 전송할 데이터를 생성하는 코드이다.
- 지금은 대략적으로만 이렇게 알고 넘어가자.

main.js 자바스크립트 파일에 코드를 넣고 터미널에서 해당 파일을 Node.js로 실행시킨다.

```
node main.js
```

웹브라우저 주소창에 localhost:3000 을 입력하여 결과를 확인한다.

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

  - **http**
    - protocol, 프로토콜, 통신 규칙으로 http를 사용한다.
    - 사용자가 서버에 접속할 때 어떤 방식으로 통신할 것인지를 나타낸다.
    - http는 웹브라우저와 웹서버가 서로 데이터를 주고 받기 위해 만들어진 통신 규칙이다.
  - **opentutorials.org**
    - host 또는 domain name
    - 인터넷에 연결된 특정 컴퓨터의 주소이다.
  - **3000**
    - 포트 번호
    - 한 대의 컴퓨터에 여러 서버가 있는 경우 클라이언트가 서버에 접속했을 때 어떤 서버와 통신할지가 애매하다.
    - 클라이언트가 서버에 접속할 때 포트번호를 명시하면 해당 포트번호에 연결된 서버와 통신하게 된다.
  - **main**
    - path
    - 컴퓨터 안에 있는 어떤 디렉터리의 어떤 파일인지를 가리킨다.
  - **?id=HTML&page=12**
    - query string
    - Query string을 사용해 서버에게 정보를 전달한다. 이 정보는 id 값이 HTML이고 page 값이 12이라는 것을 나타낸다.
    - query string은 물음표(?)로 시작하는 걸로 약속되어 있다.
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

- 결과를 확인하면 에러가 발생하지만, queryData가 객체인 것을 확인할 수 있다.
  - { id: 'HTML' }
  - queryData에는 query string이 객체 형식으로 들어온다는 것을 알 수 있다.
  - queryData.id 확인 결과 HTML인 것을 알 수 있다.
- **response.end(queryData.id)**
  - query string에 따라 다른 정보를 웹페이지에 출력한다.
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

코드 설명

```js
var title = queryData.id;
```

- queryData는 URL의 query string을 객체 형식으로 저장한다.
- queryData 객체의 id의 값을 title 변수에 저장한다.
  - URL의 query string에서 값 이름을 id로 사용하므로, title 변수의 값은 query string에서의 id의 값이다.
  - 예를 들어 URL을 localhost:3000/?id=HTML 으로 사용하면 title의 값은 HTML이다.
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
- 첫 번째 인자: `data/${queryData.id}`
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

URL 분석 코드의 결과를 확인한다.

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