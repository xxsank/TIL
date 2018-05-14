# 5/14(월)

## 1. Today I learned

### 1-1. 큐, 스택

#### 큐
- 데이터를 집어넣을 수 있는 선형 자료형
- **먼저 들어간 데이터가 먼저 나오는 방식이다** FIFO 방식(선입선출)
- 자바스크립트에서 배열로 구현한 Queue
  ```js
    class Queue {
      constructor() {
        this._arr = [];
      }
      enqueue(item) {
        this._arr.push(item);
      }
      dequeue() {
        return this._arr.shift();
      }
    }

    const queue = new Queue();
    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.dequeue(); // 1
  ```
  - 순서대로 처리해야 하는 작업을 임시로 저장하는 **버퍼** 역할로 쓰인다.

#### 스택
- 큐와 비슷한 동작방식
- **나중에 집어넣은 데이터가 먼저 나오는 방식이다** LIFO(후입선출)
- 자바스크립트에서 배열로 구현한 Stack
  ```js
  class Stack {
    constructor() {
      this._arr = [];
    }
    push(item) {
      this._arr.push(item);
    }
    pop() {
      return this._arr.pop();
    }
    peek() {
      return this._arr[this._arr.length - 1];
    }
  }

  const stack = new Stack();
  stack.push(1);
  stack.push(2);
  stack.push(3);
  stack.pop(); // 3
  ```
  - **이전 작업내용을 저장해 둘 필요가 있을때 사용된다.** 예를들어 커밋,되돌리기 등등비슷한 개념
### 1-2. 비동기 프로그래밍
- 프로그래머 사이들에서 굉장히 핫한 주제이다.
- 비동기 프로그래밍을 사용하면 성능을 좀 더 향상 시킬수 있다.

#### 타이머 API
- 수를 특정 시간이 지난 뒤에 실행시키거나, 혹은 함수를 주기적으로 실행시키는 작업
  ```js
  setTimeout(() => {
    console.log('setTimeout이 실행된 지 2초가 지났습니다.');
  }, 2000);

  setInterval(() => {
    console.log('3초마다 출력됩니다.');
  }, 3000);
  ```
  - 위에 두 함수는 많이 쓰인다.
  - 각각 **타이머 식별자**를 반환한다.
    ```js
    const timeoutId = setTimeout(() => {
    console.log('setTimeout이 실행된 지 2초가 지났습니다.');
    }, 2000);

    const intervalId = setInterval(() => {
      console.log('3초마다 출력됩니다.');
    }, 3000);

    clearTimeout(timeoutId);  /*실행을 멈추게한다*/
    clearInterval(intervalId);
    // 아무것도 출력되지 않습니다
    ```

##### 타이머 사용 시 주의할 점
- `setTimout`과 `setInerval`은 아주 정확한 지연시간을 나타내지는 않는다.

#### 브라우저의 JavaScript 코드 실행 과정

##### 호출 스택(Call Stack)
- 호출 스택은 스택형태의 저장소로 JavaScript엔진은 함수 호출과 관련된 정보를 이 곳에서 관리한다.
- 호출 스택에 저장되는 각 항목을 **실행 맥락** 이라 부른다.
- 아래와 같은 정보들이 저장됨.
  - 함수 내부에서 사용되는 변수
  - 스코프 체인
  - `this`가 가리키는 객체

##### 작업 큐 (Task Queue)
- JavaScript는 단일 thread 이다. Call Stack을 하나밖에 가지지 않음. 함수를 하나밖에 실행하지 못함.

#### 비동기 프로그래밍
- 어떤 일이 완료되기를 기다리지않고 다음 코드를 실행해 나가는 프로그래밍을 방식을 **비동기 프로그래밍**이라 한다.
- 반대로 어떤 일이 완료될때까지 실행을 멈추고 기다리는 것을 **동기식 프로그래밍** 이라한다.
ㅈ- 브라우저에서의 비동기 프로그래밍은 주로 **통신, 계산**과 같이 오래 걸리는 작업들을 브라우저에 위임할 때 이루어진다.

##### 콜백
- 콜백은 다른 함수의 인수로 넘기는 함수를 말함, 이 콜백을 가지고 비동기 프로그래밍을 할 수 있다.

##### promise
- 순수하게 콜백만 사용했을 때는, 데이터 흐름이 조금만 복잡해져도 코드가 복잡해지기 때문에 이 문제를 해결하기위한 라이브러리들이 등장했고, 그 중에서 개발자들에게 널리 선택받은 것이 바로 Promise 패턴을 사용한 라이브러리들이 있었으나, 이 라이브러리들이 표준화 되어 결국, ES2015에 이르러 JavaScript 언어 자체에 포함되게 되었다.
- Promise는 '언젠가 끝나는 작업'의 결과값을 담는 통과 같은 객체이다. `then` 메소드를 통해 콜백을 등록해서, 작업이 끝났을때 결과값을 가지고 추가 작업을 할 수 있다.
- Promise 객체를 생성하는 가장 쉬운 방법은 `Promise.resolve` 정적 메소드를 사용하는 것 이다.
  ```js
  const p = Promise.resolve(1);
  ```
  - 위 코드에서 `1`이라는 결과 값을 갖는 Promise 객체를 생성했지만, 이 코드는 비동기 작업을 하고 있지는 않는다.

  ```js
  const p = new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('2초가 지났습니다.');
      resolve('hello');
    }, 2000);
  });
  ```
  - `Promise` 생성자는 콜백을 인수로 받음, 이 콜백의 첫 번째 인수로 `resolve` 함수가 들어온다. `resolve`를 호출하면 `resolve`에 인수로 준 값이 곧 **Promise 객체의 궁극적인 결과값이 된다**
  - `reject`함수는 비동기 작업에서 에러가 발생했을때 호출 하는 함수.

- `fetch`: 최신 브라우저에는 HTTP 통신을 위한 `fetch` 함수가 내장되어있다. 이 함수는 Promise 객체를 반환.
- `then` 메소드는 Promise 객체를 반환하므로, 콜백을 중첩하지 않고도 비동기 작업을 연이어 할 수 있다.
- 비동기 작업이라는 동작 자체를 **값으로 다룰수 있게됨**

#### 비동기 함수
- ES2017에서 도입된 **비동기 함수**를 사용하면, 동기식 코드와 거의 같은 구조를 갖는 비동기식 코드를 짤 수있다.
- 함수 앞에 `async` 키워드를 붙이면, 이 함수는 비동기 함수가 된다.
  ```js
  // 비동기 함수
  async function func1() {
    // ...
  }

  // 비동기 화살표 함수
  const func2 = async () => {
    // ...
  }

  // 비동기 메소드
  class MyClass {
    async myMethod() {
      // ...
    }
  }
  ```
  - 비동기 함수는 항상 **Promise 객체를 반환**
  - `then` 메소드와 똑같은 방식으로 동작.

- `await`: Promise 의 `then` 메소드와 유사한 기능을 하며, `await` 키워드 **뒤에 오는 Promise가 결과값을 가질 때까지 비동기 함수의 실행을 중단시킵니다.**
  - `await`은 연산자 이기도하며, `await` 연산의 결과 값은 뒤에오는 **Promise 객체의 결과값**이 된다.

  ## 2. Today I found out
- 비동기 처리와 promise의 개념이 완전하게 잡히지 않았다. 생소한 개념들이며 후에 통신을 이용한 작업들을 사용할때 standard가 되는 개념 처렴 느껴저 두고두고 복습해야 할 필요가 있을 것 같다.

## 3. Ref
- [비동기처리,promise 관련 설명 사이트](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)