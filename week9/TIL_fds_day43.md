# 5/16(수)

## 1. Today I learned

### 1-1. Web Form 

#### HTML form의 기본 동작
- HTML form을 전송하면, 입력된 정보가 기본적으로 **percent encoding** 되어 요청됨
  - GET method
    ```js
    GET /search?query=%EA%B0%9C&sort=latest HTTP/1.1
    ...
    ```
  - POST method
    ```js
    POST /form HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    ...

    home=Cosby&favorite+flavor=flies
    ```

#### multipart/form-data
- 기본 설정(percent encoding)으로는 폼으로 **파일을 업로드**하는 것은 불가능
- (클라이언트 측) form 태그에 `enctype="multipart/form-data"` 속성을 적용하면 파일 업로드 가능
- (서버 측) body-parser 미들웨어는 `multipart/form-data` 형태의 요청을 지원하지 않음 (multer 필요)

#### UUID
- 인터넷 상의 수많은 자료를 구분하기 위해 각 자료에 식별자를 부여하는 일은 아주 중요하다, 식별자를 부여하는 가장 쉬운방법은 자료가 생성된 순서대로 번호를 붙이는 것인데, UUID는 표현할 수 있는 경우의 수가 많다. (128bit = 2의 128제곱) UUID 난수를 생성하는 표준적인 방법(UUID version 4)을 사용하면, 언제 어디서 UUID를 생성해도 정확히 같은 UUID가 생성될 수 있는 확률이 매우매우매우매우 작기 때문에 안심하고 식별자로 사용할 수 있다.

#### POST method
- HTML form은 기본적으로 GET과 POST 밖에 지원하지 않으므로, 순수 HTML만을 사용해서 웹 서비스를 구현한다면 자료의 수정이나 삭제를 할 때 POST method를 사용해야 한다.

#### 기타
- `validation` - 서버측은 반드시 validation을 해주어야 한다
- `URL Shortener` - 긴 URL을 폼에 입력후 작은 URL로 바꿔 주는 것
- `morgan` - 터미널에 텍스트 기능을 보여주는 라이브러리
- express는 먼저 등록한 라우터 핸들러가 우선순위가 더 높다.
- 오늘 수업의 중요 point
  - 환경변수를 통해서 서버 실행시에 설정을 넣어줄수있다.
  - hidden type의 input태그를 통해서 사용자의 정보를 보여주지 않고 서버에 넘겨줄수 있다.

## 2. Today I found out

## 3. Ref
[bit.ly](https://bitly.com/)
[301 vs 302 리디렉트(redirect)](http://www.seo-korea.com/301-vs-302-redirect/)