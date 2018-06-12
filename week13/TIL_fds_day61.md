# 6/11(월)

## 1. Today I learned

### 1-1 JavaScript

#### 예외 처리
- JavaScript에는 코드 실행 중에 예기치 못한 에러가 발생했을 때, 이로부터 코드의 실행 흐름을 복구할 수 있는 기능이 내장되어 있습니다. 이런 기능을 일러 예외 처리(exception handling)라고 한다.

- **동기식 코드에서의 예외 처리**
  - 코드 실행 중에 에러가 발생하면, 코드의 실행이 중단되어 그 시점에 실행 중이었던 작업을 완료할 수 없게 된다.

  - 일반적으로 에러가 났을 경우에는 그 다음 코드는 실행되지 않지만 `try...catch...finally` 구문을 사용하면 에러가 나더라도 코드의 실행을 지속할 수 있다.

    ```js
      try {
        console.log('에러가 나기 직전까지의 코드는 잘 실행됩니다.');
        new Array(-1); /* RangeError: Invalid array length*/
        console.log('에러가 난 이후의 코드는 실행되지 않습니다.');
      } catch (e) {
        console.log('코드의 실행 흐름이 catch 블록으로 옮겨집니다.');
        alert(`다음과 같은 에러가 발생했습니다: ${e.name}: ${e.message}`);
      }
    ```

    - 에러가 났을 때 원상복구를 시도할 코드를 `try` 블록 내부에 작성하면, 에러가 발상했을때 코드의 실행 흐름이 `try`블록에서 `catch`블록으로 옮겨간다.
  
  - 에러가 나던 안나던 실행시켜야하는 코드들은 `finally` 블록안에 넣어주면 에러 발생 여부와 관계 없이 **무조건** 실행 된다. `try` 블록 내에서 `return`,`break`,`continue` 등 으로 인해 코드의 실행 흐름이 즉시 이동될 때에도 마찬가지이다.

  - `finally` 블록은 `catch` 블록과도 같이 사용된다.
    - 에러가 안 났을 때: `try` - `finally`
    - 에러가 났을 때: `try` - **에러 발생** - `catch` - `finally`

    ```js
      try {
      console.log('try');
      new Array(-1); /* RangeError: Invalid array length*/
    } catch (e) {
      console.log('catch');
    } finally {
      console.log('finally');
    }
    ```

- **직접 에러 발생시키기**
  - `Error` 생성자와 `throw` 구문을 사용해서 프로그래머가 직접 에러를 발생시킬 수 있다.

    ```js
    const even = parseInt(prompt('짝수를 입력하세요'));
    if (even % 2 !== 0) {
      throw new Error('짝수가 아닙니다.');
    }
    ```
  
  - 특이한 기능을 가진 객체

  - 직접 에러를 만들어서 던질수도 있고, `try` `catch`블록으로 감싸서 던질수도 있다.

  - `MyError` 클래스를 통해 에러 객체를 생성할 때 에러에 대한 상세정보를 포함시키면, `catch`블록 안에서 원상복구를 위해 이 값을 활용할 수 있다.

    ```js
    class MyError extends Error {
      constructor(value, ...params) {
        super(...params);
        this.value = value;
        this.name = 'MyError';
      }
    }

    try {
      const even = parseInt(prompt('짝수를 입력하세요'));
      if (even % 2 !== 0) {
        throw new MyError(even, '짝수가 아닙니다.');
      }
    } catch (e) {
      if (e instanceof MyError) {
        console.log(e.value);
      }
    }
    ```
      - 자체 에러 생성자를 만들어서 사용할 수 있다.

- **비동기식 코드에서의 예외 처리**
  - **비동기 콜백**
    - 비동기식으로 작동하는 콜백의 내부에서 발생한 에러는, 콜백 바깥에 있는 `try` 블록으로는 잡아낼 수 없다.
    ```js
    try {
      setTimeout(() => {
        throw new Error('에러!');
      });
    } catch (e) {
      console.error(e);
    }
    ```
    - error는 호출스택과 관련이 있다.
  
  - **Promise**
    - pending - Promise 객체에 결과값이 채워지지 않은 상태
    - fulfilled - Promise 객체에 결과값이 채워진 상태
    - rejected - Promise 객체에 결과값을 채우려고 시도하다가 에러가 난 상태
    
    ```js
    const p = new Promise(resolve => {
      const even = parseInt(prompt('짝수를 입력하세요'));
      if (even % 2 !== 0) {
        throw new Error('짝수가 아닙니다.');
      } else {
        resolve(even);
      }
    });

    p.then(even => {
      return '짝수입니다.';
    }, e => {
      return e.message;
    }).then(alert);
    ```

  - **비동기 함수**
    - Promise 객체의 예외 처리 방식은, 일반적인 동기식 예외 처리 방식과 다르게 콜백을 사용하고 있어서 코드를 복잡하게 만드는 원인이 된다.

    - 비동기 함수 내부에서는, rejected 상태가 된 Promise 객체를 동기식 예외 처리 방식과 동일하게 `try...catch...finall` 구문으로 처리할 수 있다.
    
    ```js
    async function func() {
      try {
        const res = await fetch('https://nonexistent-domain.nowhere');
      } catch (e) {
        console.log(e.message);
      }
    }

    func(); // 출력 결과: Failed to fetch
    ```
    - 동기식 코드처럼 작성할 수 있다.
    - Promise 객체에 대해 `await` 구문을 사용하지 않는 경우 에는 에러가 잡히지 않는다.

#### 모듈
- ES2015는 모듈이라는 시스템이 있는데 `script` 태그에 `type="module"` 어트리뷰트를 추가해주면, 이 파일은 모듈로서 동작한다. 파일 확장자로는 대개 `mjs`가 사용됨.

  ```js
  <script type="module" src="index.mjs"></script>
  ```

- Webpack, Parcel 등의 모듈 번들러를 통해 변환과정을 거친 뒤, 브라우저에는 일반적인 JavaScript 파일로서 불러오는 방법이 널리 사용되고 있는 추세이다.
- 모듈번들러는 모든 JavaScript 파일을 하나로 합쳐주는 프로그램이다. 모듈이아니라 일반적인 JavaScript 파일을 사용할수 있게 만들어줌.

- **모듈이란?**
  - JavaScript 코드를 담고 있는 파일
  - import 혹은 export 구문을 사용할 수 있다.
  - 별다른 처리를 해주지 않아도 엄격 모드(strict mode)로 동작한다.
  - 모듈의 가장 바깥쪽에서 선언된 이름은 전역 스코프가 아니라 **모듈 스코프**에서 선언된다.

- **모듈 스코프**
  - 모듈 내부의 가장 바깥 스코프에서 이름을 선언하더라도, 전역 스코프가 아니라 모듈 스코프에서 선언된다.
    ```js
    // variables.js

    const foo = 'bar';

    /* 이 파일이 모듈로서 사용되고 있다면, `undefined`가 출력됩니다.*/
    console.log(window.foo);
    ```

- **export & import**
  - 모듈 스코프에서 정의된 이름은 **export** 구문을 통해 다른 파일에서 사용할 수 있다.
  ```js
  // variables.js
  const foo = 'bar';
  const spam = 'eggs';

  // foo, spam을 다른 파일에서 사용할 수 있도록 export 해주었습니다.
  export { foo, spam };
  ```
  - export를 하고 다른 파일에서 import 구문을 통해 가져온뒤 사용할 수 있다.

  ```js
  // main.js

  // variables 모듈에 선언된 이름을 사용하기 위해 import 해주었습니다.
  import { foo, spam } from './variables.js';

  console.log(foo);
  console.log(spam);
  ```

- **선언과 동시에 export 하기**
  - 이름을 선언할때 앞에 `export`를 붙혀서 선언과 `export`를 한꺼번에 할 수도 있다.
  ```js
  // common.js
  export const foo = 'bar';
  export const spam = 'eggs';
  export function add(x, y) {
    return x + y;
  }
  export class Person {
    // ...
  }
  ```

- **default export**
  - `export default` 구문을 통해, 모듈을 대표하는 하나의 값을 지정하고 그 값을 다른 모듈에서 편하게 불러와서 사용가능하다. 중괄호 없이 import함.
  ```js
  // foo.js

  export default 'bar';

  /****************************/
  /****************************/

  // main.js

  import foo from './foo.js'

  console.log(foo); // bar
  ```

  - 함수 표현식이나 클래스 표현식도 사능가능
  - 모듈에는 default export는 하나만 정의 가능하다.
  - named export는 여러개 정의가능.
  ```js
  // `React`라는 이름의 default export와,
  // Component, Fragment라는 일반적인 export를 동시에 가져오기
  import React, { Component, Fragment } from 'react';
  ```

- **다른 이름으로 export & import 하기**
  - `export` 혹은 `import` 하는 이름의 뒤에 as를 붙여서, 다른 이름이 대신 사용되게 할 수 있다.
    ```js
    const foo = 'bar';
    export { foo as FOO }; // FOO 라는 이름으로 export 됩니다.  
    ```

- **모듈 사용 시 주의할 점**
  - 같은 모듈을 여러 다른 모듈에서 불러와도, 모듈 내부의 코드는 단 한 번만 실행된다.

  - import 구문과 export 구문은 모듈의 가장 바깥쪽 스코프에서만 사용할 수 있다.
  
  - ECMAScript 공식 명세에는 모듈을 불러오는 방법에 대한 내용이 포함되어있지 않고, 이와 관련된 내용을 전적으로 모듈 구현체에 맡긴다. 따라서, 모듈을 어떤 환경에서 실행하느냐에 따라서 구체적인 로딩 순서나 동작방식이 조금씩 달라질 수 있다.

## 2. Today I found out
- 컴포넌트를 분리하는 이유는 알겠는데, 코드의 동작 흐름이 헷갈리고 어떻게 분리해야 될지 감이 잡히질 않는다. 컴포넌트 부분을 좀 더 공부하는 방향으로 학습해야겠다. 
