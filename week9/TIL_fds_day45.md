# 5/16(수)

## 1. Today I learned

### 1-1. Express Middleware

#### Middleware
- 모든 미들웨어는 **함수**, 즉 안에서 어떤 작업이든 가능
- request 객체, response 객체, **next 함수**를 인자로 받음
- request 객체, response 객체를 조작해서 기능 구현
- 다음 미들웨어를 동작시키기 위해 next 함수를 인자없이 호출
- 등록된 순서대로 실행된다.
- Express에만 있는 개념이다.
- 응답을보내주거나 next를 호출하는것 두개중에 하나를 곡 해주어야한다.

#### app.use
- 미들웨어를 앱 전체에서 동작하도록 주입하거나
  ```js
  app.use(helloMiddleware)
  ```
- 특정 경로에서만 동작하도록 주입 
  ```js
  app.use('/some-path', helloMiddleware)
  ```
- 한 번에 여러 개 주입
  ```js
  app.use(middleware1, middleware2, middleware3, ...)
  ```

### 1-2 Cookie

#### 쿠키의 필요성
- 개별 클라이언트의 여러요청에 걸친 정보의 유지 
  - 장바구니
  - 로그인/로그아웃
  - 방문기록
  - ...

#### HTTP Cookie
- 쿠키란 것은 서버가 응답을 통해 웹 브라우저에 저장하는 이름+ 값 형태의 정보
- 웹 브라우저는 쿠키를 저장하기 위한 저장소를 가지고 있음
- 저장소는 자료의 유효기간과 접근 권한에 대한 다양한 옵션을 제공

#### Set-Cookie Option
- `Expires`,`Max-Age` : 쿠키의 지속 시간 설정
- `Secure` : HTTPS를 통해서만 쿠키가 전송되도록 설정
- `HttpOnly` : 자바스크립트에서 쿠키를 읽지 못하도록 설정
- `Domain`, `Path` : 쿠키의 scope 설정(쿠키가 전송되는 URL을 제한)

### 1-3 Ajax

#### Ajax
- 비동기적인 웹 어플리케이션의 제작을 위한 클라이언트 측 웹 개발 기법.... 을 뜻하나 요즈음은 의미가 변형되어 웹 브라우저에서 **XMLHttpRequest** 혹은 **fetch**를 이용해서 보내는 HTTP 요청을 통칭하기도 함ㅔ
- 자바스크립트로 보내는 HTTP 요청

#### Ajax의 장점
- 화면 전체를 다시 로드하지않고 내용을 갱신할 수 있어 더 나은 사용자 경험 제공
- 서버의 응답을 기다리는 동안에도 여전히 웹 어플리케이션을 사용 가능
- 필요한 자원만 서버에서 받아오게 되므로 트래픽이 줄어듬

#### Ajax의 단점
- 클라이언트 구현이 **굉장히** 복잡해짐

#### Axios
- Promise based HTTP client
- 브라우저와 Node.js에서 모두 사용가능
- XMLHttpRequest. fetch에 비해 사용하기 편하고 기능이 더많다.

### 1-4 Json-Server

#### Json-Server
- json-server는 json 파일을 사용하여 간단한 시뮬레이션을 위한 REST API Mock server를 구축할 수 있는 툴이다.

- Create a `db.json` file
  ```js
  {
    "posts": [
      { "id": 1, "title": "json-server", "author": "typicode" }
    ],
    "comments": [
      { "id": 1, "body": "some comment", "postId": 1 }
    ],
    "profile": { "name": "typicode" }
  }
  ```
- Start JSON Server
  ```
  // 기본포트는 3000이다.
  $ json-server --watch db.json
  ```
## 2. Today I found out

## 3. Ref