# 4/18(수)

## 1. Today I learned

### 1-1. 함수 더 알아보기
  
#### 객체로서의 함수
- 함수 `Function` 생성자로 부터 생성되는 객체이다, 객체와는 다르게 호출할 수 있다는 특징이있다.
- 함수 객체 두 가지 유용한 속성
  - `length` : 함수의 매개변수의 개수를 반환.
  - `name` : 함수의 이름을 반환, 변수에 익명함수를 대입했을 때는 변수의 이름이 바로 함수 이름으로 반환.(면접문제에 나올 정도로 중요하지는 않음.)
    ```js
    function add(x, y) {
      return x + y;
    }
    console.log(add.length); // 2
    console.log(add.name); // add
    ```

#### 주인 없는 this
- `this`는 생성자 혹은 메소드에서 객체를 가리킬때 쓰인다.
- 생성자나 메소드가 아닌 함수에서 `this`를 사용한다 해서 에러가 나지는 않는다.
- 옛날 버전 자바스크립트에서는 `new`를 빠트린 채 생성자를 호출하면 `this`는 전역 객체를 가리키게 되어 큰 문제가 생길 수도 있었다.

#### 엄격모드
- 위 같은 주인 없는 this를 사용했을때 문제점을 방지할 수 있는 방법이 있다.
  ```js
  function Person(name) {
  // 엄격 모드를 활성화합니다.
  'use strict';

  // `undefined`의 속성을 변경하려고 하고 있기 때문에, 에러가 납니다.
  this.name = name;
  } 

  Person('john'); // TypeError: Cannot set property 'name' of undefined
  ```
- ES2015 모듈을 이용해 작성된 코드는 자동으로 엄격모드로 동작되기 때문에 매번 `use strict;`를 써주지 않아도 엄격모드로 동작한다.

#### this 바꿔치기
- `this`는 때에 따라 다른 값을 가리킨다. 우리가 원하는 값을 가리키게 만들 수도 있는데, 함수 객체의 `bind`,`call`,`apply`메소드를 이용하면 된다.
  ```js
  function printGrade(grade) {
  console.log(`${this.name} 님의 점수는 ${grade}점입니다.`);
  }

  const student = {name: 'Mary'};
  const printGradeForMary = printGrade.bind(student);

  printGradeForMary(100); // Mary 님의 점수는 100점입니다.
  ```
- `bind`는 실무에서도 꽤 쓰이니 잘 **기억**하자, 함수를 새로 생성해주는  메소드.
  ```js
  function printGrade(grade) {
  console.log(`${this.name} 님의 점수는 ${grade}점입니다.`);
  }

  const student = {name: 'Mary'};

  printGrade.call(student, 100); // Mary 님의 점수는 100점입니다.
  printGrade.apply(student, [100]); // Mary 님의 점수는 100점입니다.
  ```
- `call`,`apply` 메소드는 함수를 새로 생성해주지는 않지만 호출하는 메소드이다.(임시적으로 `this`를 바꿔치기 한 후에 호출) **자주쓰이지는 않는다.** 
- `apply`는 인수를 배열로 넘겨줘야 한다. 나머지 기능은 동일

#### arguments
- `function` 구문을 통해 생성된 함수가 호출될 때는 `arguments`라는 변수가 함수내부에 자동으로 생성된다. **배열은 아님!**
- ES2015 이전까지 인수의 개수에 제한이 없는 함수를 정의 하는데 사용되었음.
- ES2015에서 도입된 나머지 **매개변수** 문법을 통해 똑같은 기능을 더 깔끔한 문법으로 구현할 수 있으므로, `argumetns`는 더 이상 **사용하지** 않는다.
  - ```js
    function sum(...ns) {
    let result = 0;
    for (let item of ns) {
      result += item;
    }
    return result;
    }

      sum(1, 2, 3, 4); // 10
    ```

  - 매개변수 앞에 `...`을 붙여 주면 해당 매개변수에 모든 인수가 저장됨, `arguments`와 달리 나머지 매개변수는 **실제 배열** 이기 때문에, 배열 메소드도 사용가능하다. 
  - 나머지 매개변수는 매개변수 목록에 제일 **뒤**에 위치해야한다.

#### 화살표 함수
- ES2015에 도입된 새로운 유형의 함수, `(매개변수 목록) => {함수 내용}`과 같은 문법을 통해 정의한다.
- 익명함수로밖에 정의 할 수 없음.
- 특정 조건을 만족하는 화살표 함수
  - 화살표 함수의 매개변수가 하나라면 , **괄호를 생략**할 수 있다. 
  - 화살표 함수의 내부가 **하나의 구문**으로 이루어져있다면, **중괄호를 생략** 할 수 있다, 이 때 이 구문의 결과값이 곧 함수의 반환값이 된다
    - 예시
      ```js
      const add = (x, y) => x + y;
      const negate = x => !x;
      ```
- `function` 문법 함수로 정의 됐을때는 특별한 성질을 갖고 있다.
  - 화살표 함수는 `생성자`로 사용될 수 없다.
  - `prototype` 속성도 갖지 않는다.
  - 화살표 함수는 스스로의 `this`,`arguments`,`super`를 가지지 않는다.
  - 함수 내부에서 `yield` 키워드를 사용할 수 없다. 즉, 제너레이터로 사용될 수 없다. 
- 화살표 함수는 생성되는 순간 `this`가 결정되어있다.(즉 `this`가 안바뀜)
- `function` 문법 함수는 어떻게 호출하느냐에 따라 `this`가 결정된다.

#### 매개변수의 기본값
- 함수 호출 시에 인수를 주지 않으면 매개변수에는 `undefined`가 대입된다. 인수가 주어지지 않았을 때는 미리 설정된 값을 사용하는 함수를 작성할 수 있다.
  ```js
  function hello(name) {
  // 매개변수는 `var` 변수와 같은 성질을 갖기 때문에, 재대입을 할 수 있습니다.
  if (name === undefined) {
    name = 'Mary';
  }
  console.log(`Hello, ${name}!`);
  }

  hello('John'); // Hello, John!
  hello(); // Hello, Mary!
  hello(undefined); // Hello, Mary!
  ```

## 2. Today I found out
- this는 다른언어에서 클래스와 함께 많이 써보았지만 어떤식으로 동작하는지는 자세하게까지는 몰랐는데 이번 수업시간에 그 this에 대한 정의를 다시한번 제대로 공부할수 있게 되서 좋았습니다.
  
## 3. Ref