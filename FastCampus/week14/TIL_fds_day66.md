# 6/18(월)

## 1. Today I learned

### 1-1 React

#### **children prop**

#### **로그인 시 예외처리**
- 네트워크 요청이 일어난 부분들은 `try ~ catch` 구문으로 감싸주는게 좋다.

- Axios의 error 처리 방법
  ```js
  axios.get('/user/12345')
    .catch(function (error) {
      if (error.response) {
        // The request was made and the server responded with a status code
        // that falls out of the range of 2xx
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.headers);
      } else if (error.request) {
        // The request was made but no response was received
        // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
        // http.ClientRequest in node.js
        console.log(error.request);
      } else {
        // Something happened in setting up the request that triggered an Error
        console.log('Error', error.message);
      }
      console.log(error.config);
    });
  ```

#### **제어되지 않는 컴포넌트**
- 

#### **Presentational component & Container component**
- **Presentational component** : 화면표시만을 위한 컴포넌트 
  - 외부세계와 직접 연동 되진 않지만 `prop`을 통해 간접적으로 연동될 수도 있다.
  - 어떻게 연동되는지에 따라 다목적으로 사용이 가능.
  - 중립적인 인터페이스이어야 한다. (**재사용성이 높아지기 떄문**)
  - 외부세계와 연동되지않게 설계하는것이 좋음.
- **Container component** : 외부세계와 연동되는 컴포넌트 

- `stories` : Presentational component의 테스트를 도와주는 도구