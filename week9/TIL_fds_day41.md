# 5/14(월)

## 1. Today I learned

### 1-1. 큐, 스택, 트리

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




### 1-3. SASS