# 5/15(화)

## 1. Today I learned

### 1-1. HTTP 

#### HTTP
- **웹 브라우저와 웹 서버 간의 통신**을 위해 개발된 통신규약
- 최근에는 **REST API의 부상**과 함께 다른 용도로도 널리 사용 된다.
  - 모바일 앱 - 서버 간 통신
  - 서버 - 서버 간 통신
- **80번 포트**를 기본으로 사용
- 클라이언트의 **요청(request)**과 서버의 **응답(response)으로 이루어짐

#### 역사
- **1991**
  - HTTP 초기버전 발표, **텍스트만 전송** 할 수 있는 극도로 단순한 프로토콜. 1990년대 초 인터넷 붐을 일으킴
- **1996**
  - 여러 인터넷 서비스 업체들이 자체적으로 사용하던 HTTP 구현들을 모아 HTTP 1.0 발표

- **1999**
  - 1.0의 문제를 해결하고 여러가지 기능을 추가한 HTTP 1.1을 발표. **현재까지 사용되고 있는 버전**

#### HTTPS 
- HTTP over SSL
- HTTP 통신을 암호화해 주고받는 내용을 중간에서 가로챌 수 없도록 함
- **443번 포트**를 기본으로 사용

#### HTTP/2
- **구글의 SPDY 프로토콜** 기반으로 2015년에 확정된 새로운 HTTP 표준
- **속도 개선**에 중점을 두고 개발됨
- **반드시 HTTPS를 사용해야 함**
- 현재 전체 웹사이트 중 26% 이상이 사용중

#### HTTP 구성요소
- Request & Response
  - 웹 브라우저(또는 다른 클라이언트)는 웹 서버에 요청(request)를 보냄
  - 그에 따라 서버는 클라이언트 응답(respose)를 보냄
  - 웹 브라우저의 경우, **HTML 문서 형태의 응답**이 오면 해당 문서를 분석한 후, **문서에 포함된 모든 자원에 대한 요청을 각각 추가로 보냄**(이미지,동영상, 오디오,CSS,JS......)

#### Request Methods
- HTTP 명세에는 8종류가 등록되어 있고, 각각의 역할과 충족해야 하는 성질이 명시되어 있다.
- 웹 브라우저는 **특정 상황에서 특정 메소드로 요청을 보내도록 만들어져 있음**
- Ajax와 같이 **요청을 보내는 코드를 직접 짤 때**는 요청 메소드를 선택할 수 있음
- **자료의 본문을 요청하는 GET** 메소드와, **새로운 자료를 등록하는 POST** 메소드가 가장 많이 쓰임

#### Percent Encoding
- URL은 **ASCII(128갱의 영문자+특수문자+제어문자)밖에 사용하지 못하기 때문에, non-ASCII문자를 위한 표현방법이 필요함
- Percent encoding은 non-ASCII 문자를 위한 웹표준 인코딩 방법으로, JavaScript에 관련 기능이 포함되어 있다.

#### Response Status
- 응답의 성공, 실패 여부와 종류를 나타냄
- status category
  - 2xx : 성공
  - 3xx : 추가 작업이 필요함
  - 4xx : 실패 - 클라이언트 책임
  - 5xx : 실패 - 서버 책임 

- **status code - 2xx**
  - 200 OK : 성공
  - 201 Created : 자료가 성공적으로 생성됨
- **status code - 3xx**
  - 301 Moved Permanently (Redirection) : 자료가 완전히 다른 곳으로 이동했음
  - 302 Found(Redirection) : 자료가 일시적으로 다른 곳에 있음
  - 304 Not Modified(Cache) : 클라이언트가 이미 가지고 있던 자료가 수정되지 않았음(그대로 사용하면 됨)
- **status code - 4xx**
  - 400 Bad Request : 요청의 형태가 잘못되어 응답할 수 없음
  - 403 Forbidden : 요청한 자료에 접근할 권한이 없음
  - 404 Not Found : 요청한 자료가 없음
- **status code - 5xx**
  - 500 Internal Server Error : 요청을 처리하던 중에 예상치 못한 오류가 발생함
  - 503 Service Unavailable : 서버가 일시적으로 응답을 할 수 없음

#### Header
- **요청과 응답**에 대한 **추가 정보**를 표현하는데 사용됨
- 인증,캐싱,쿠키,보안,내용협상,프록시 등 웹 표준에 정의된 많은 **기능을 제어** 하는데 사용됨
  - Authorization : 요청의 인증 정보
  - User-Agent : 요청 중인 클라이언트의 정보
  - Location : 301, 302 응답에서 자료의 위치
  - Accept : 요청이 어떤 형태의 자료를 원하는지 나타냄
  - Content-Type : 요청 혹은 응답이 어떤 형태의 자료인지 나타냄

#### Content Negotiation
- 요청의 Accept, Accept-Language 등의 헤더를 보고 서버가 그에 맞는 형태의 자료를 응답하는 절차를 content negotiation(내용협상)이라고 함

### 1-2. Express

#### Express
- Node.js 생태계에서 **가장 널리 쓰이는 웹 프레임워크**
- 내장하고 있는 기능은 매우 적으나, **미들웨어**를 주입하는 방식으로 기능을 확장하는 **생태계**를 가지고 있음

#### Express 앱의 기본 구조
  ```js
  // Express 인스턴스 생성
  const app = express()

  // 미들웨어 주입
  app.use(sessionMiddleware())
  app.use(authenticationMiddleware())

  // 라우트 핸들러 등록
  app.get('/', (request, response) => {
    response.send('Hello express!')
  })

  // 서버 구동
  app.listen(3000, () => {
    console.log('Example app listening on port 3000!')
  })
  ```

#### Routing
  ```js
  // HTTP 요청 메소드(GET, POST, ...)와 같은 이름의 메소드를 사용
  app.get('/articles', (req, res) => {
    res.send('Hello Routing!')
  })
  // 특정 경로에만 미들웨어를 주입하는 것도 가능
  app.post('/articles', bodyParserMiddleware(), (req, res) => {
    database.articles.create(req.body)
      .then(() => {
        res.send({ok: true})
      })
  })
  // 경로의 특정 부분을 함수의 인자처럼 입력받을 수 있음
  app.get('/articles/:id', (req, res) => {
    database.articles.find(req.params.id) // `req.params`에 저장됨
      .then(article => {
        res.send(article)
      })
  })
  ```

#### Request 객체
- `req.body` : 요청 바디를 적절한 형태의 자바스크립트 객체로 변환하여 이곳에 저장(body-parser 미들웨어에 의해 처리됨)
- `req.ip` : 요청한 쪽의 IP
- `req.params` : route parameter
- `req.query` : query string이 객체로 저장됨

#### Response 객체
- `res.stauts(..)` : 응답의 상태 코드를 지정하는 메소드
- `res.append(..)` : 응답의 헤더를 지정하는 메소드
- `res.send(..)` : 응답의 바디를 지정하는 메소드 인자가 **텍스트**면 **text/html**, **객체**면 **application/json**타입으로 응답


### 1-3. Template Language

#### 웹 초창기 - CGI
  ```js
  int main(void)
  {
    char *data;
    long m,n;
    printf("%s%c%c\n", "Content-Type:text/html",13,10);
    printf("<TITLE>Multiplication results</TITLE>\n");
    printf("<H3>Multiplication results</H3>\n");
    data = getenv("QUERY_STRING");
    if(data == NULL)
      printf("<P> Error in passing data from form to script.");
    else if(sscanf(data,"m=%ld&n=%ld",&m,&n)!=2)
      printf("<P>Error! Invalid data. Data must be numeric.");
    else
      printf("<P>The product of %ld and %ld is %ld.",m,n,m*n);
    return 0;
  }
  ```

#### Template Engine
- **템플릿과 데이터를 결합**해 문서를 생성하는 프로그램, 혹은 라이브러리
- 템플릿을 작성할 때 사용하는 언어를 **템플릿 언어**라고 함

#### EJS
- Embedden JavaScript Template
- Node.js 생태계에서 가장 많이 사용되는 템플릿 엔진
- JavaScript 코드를 템플릿 안에서 그대로 쓸 수 있음
- 예제
  ```html
  <%# index.ejs %>
  <html>
    <head>
      <title><%= title %></title>
    </head>
    <body>
      <div class="message">
        <%= message %>
      </div>
      <% if (showSecret) { %>
        <div>my secret</div>
      <% } %>
    </body>
  </html>
  ```


## 2. Today I found out

## 3. Ref
- [Brief History of HTTP](https://hpbn.co/brief-history-of-http/)

- [SPDY란](https://d2.naver.com/helloworld/140351)

- [HTTP Method Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)

- [HTTP STATUS CODES](https://httpstatuses.com/)

- [Express 공식 매뉴얼 한국어 번역](https://expressjs.com/ko/)