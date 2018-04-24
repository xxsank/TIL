# 4/24(화)

## 1. Today I learned

### 1-1. 내장 객체 및 생성자

#### JSON
- 프로그래밍을 하다보면 프로그래밍 언어에서 사용하는 자료구조를 보조기억장치에 저장하거나, 네트워크를 통해 전송해야 할 일이 생긴다. 이 때 저장/전송 가능한 형태로 변환하는 절차가 필요하며, 이 절차를 **직렬화**라함 반대로, 프로그래밍 언어에서 사용할 수 있도록 변환해주는 절차를 **역 직렬화**
- JavaScript는 아님, JavaScript 객체와 유사한 표기법을 사용하는 텍스트이다.
  ```js
  {
  "key": "value",
  "arr": [1, 2, 3],
  "nullProp": null
  } 
  ```
- JSON 내장객체의 메소드를 통해 직렬화와 역직렬화를 할 수 있다.
  - `JSON.stringify` - 텍스트로 만들어주는 직렬화 작업
  - `JSON.parse` - 객체로 다시 만들어주는 역직렬화 작업

- JSON의 속성이름을 쓸 때는 항상 `""` 큰 따옴표를 둘러 사용하자.

#### Date
- 날짜와 시각을 다루기 위한 `Date` 생성자가 내장되어 있다.
  - **협정 세계시(UTC)** - UTC가 만들어지기전에는 그리니치 평균시(GMT)라는 용어가 널리 쓰였지만, 조금씩 느려지는 지구 자전 속도에 맞추기 위해 윤초가 추가되며 세계기준으로 사용되는 시간대이다.
  - **유닉스 시간** - 컴퓨터에서 시간 데이터를 편하게 다루기 위해 쓰는 특별한 단위. 자바스크립트에서도 사용됨, POSIX 시간 또는 Epoch 시간이라는 이름으로도 불린다.

- **Syntax**
  - `new Date()` - 현재 시각을 나타내는 Date 객체 반환
  - `new Date(value)` - `value`가 정수인 경우, 밀리초 단위의 유닉스 시간으로 간주해 이에 해당하는 Date 객체 반환, 문자열일 경우 문자열이 나타내는 Date 객체 반환.
  - `new Date(year, month, day, hour, minutes, seconds, milliseconds)` - 년, 월, 일, 시, 분, 초, 밀리초를 직접 입력해서 Date 객체를 생성가능하다.
  - 엔터를 치는 시점의 시간의 객체를 만들어줌.

- **문자열로 변환하기**
  ```js
  const now = new Date();
  console.log(now.toString()); // Sun Dec 10 2017 12:49:31 GMT+0900 (KST)
  console.log(now.toLocaleString()); // 2017. 12. 10. 오후 12:49:31
  console.log(now.toDateString()); // Sun Dec 10 2017
  console.log(now.toTimeString()); // 12:49:31 GMT+0900 (KST)
  console.log(now.toISOString()); // 2017-12-10T03:49:31.145Z
  console.log(now.toUTCString()); // Sun, 10 Dec 2017 03:49:31 GMT
  ```  
- `-` 연산자를 사용해서 두 `Date` 객체 사이의 시간 간격이 얼마나 되는지 밀리초(1/1000) 단위로 측정할 수 있다.

- **라이브러리**
 - [moment.js](https://momentjs.com/) - 제일 유명하고 널리 쓰임.
 - [date-fns](https://date-fns.org/)

#### Symbol
- ES2015에서 도입된 새로운 원시 타입
- `Symbol` 내장 함수를 통해 새 심볼을 생성할 수 있음
- 새로 생성된 심볼은 다른 모든 심볼과 다른 것으로 취급된다.
- 객체의 속성 이름으로 사용되려고 만들어짐
- 마개조를 할 때 쓰임

#### Map
- ES2015에서 도입된 `Map` 생성자는 객체와 유사하게 키-값 쌍을 저장할 수 있는 새로운 자료구조를 제공한다.
  ```js
    const m = new Map();

    m.set('hello', 'world');
    console.log(m.get('hello')); /* 'world' */
    console.log(m.has('hello')); // true

    m.delete('hello');
    console.log(m.get('hello')); /* undefined */ 
    console.log(m.has('hello')); // false
  ```

- `Map` 객체는 데이터의 추가/삭제가 빈번하게 일어나는 경우 일반적인 객체보다 훨씬 빠르게 동작한다.
- JSON 등으로 직렬화 하기 어려운 특징을 가지고 있음.

#### Set
- ES2015에 도입되었고 집합 형태의 자료구조를 제공한다. `Set` 객체 내부에 이미 존재하는 데이터를 추가하려하면 무시됨. 즉 `Set` 내부에 중복된 데이터가 저장되는 것을 허용하지 않음
  ```js
  const s = new Set();

  s.add(1);
  s.add(1);
  s.add(2);

  console.log(s); // Set { 1, 2 }
  ```

- 배열과 유사한 형태의 자료구조가 필요하지만 순서가 중요하지않은경우, 중복된 데이터의 저장을 허용하지 않아야 할 경우에 고려해보자
- 실무에선 많이쓰이진 않지만 면접문제로 나옴

#### 기타
- `Proxy` - 다른 객체처럼 행세하면서, 특정한 행동에 대해서는 다른 동작방식을 보이는 새로운 객체를 만들고 싶을 때 사용합니다.

### 1-2. Iterable

#### Iterable
- 반복 가능한 객체. `for...of`구문과 함께 ES2015에서 도입. 특징은 객체의 `Symbol.iterator` 속성에 **특별한 형태의 함수** 가 들어있다는 것이다.
  ```js
  const str = 'hello';
  str[Symbol.iterator]; // [Function]
  ```
  - `Symbol.iterator` 속성에 특정 형태의 함수가 들어있다면, 이를 반복가능한 객체 혹은 줄여서 **iterable**이라고 부른다.
  - iterable객체를 만들어내는 생성자
    - `Strig`
    - `Array`
    - `TypedArray`
    - `Map`
    - `Set`

#### Iterable의 사용
- 객체가 Iterable이라면, 아래의 기능들을 사용할 수 있음
  - `for...of` 루프
  - spread 연산자(`...`)
  - 분해대입
  - 기타 iterable을 인수로 받는 함수
    ```js
    /* `for...of` */
    for (let c of 'hello') {
      console.log(c);
    }

    /* spread 연산자 */
    const characters = [...'hello'];

    /* 분해대입 */
    const [c1, c2] = 'hello';

    /* `Array.from`은 iterable 혹은 array-like 객체를 인수로 받습니다. */
    Array.from('hello');
    ```

#### Generator 함수
- 직접 iterable인 객체를 만들수도 있다.
-  Generator 함수는 iterable객체를 반환하는 특별한 형태의 함수이다.
  ```js
  // generator 함수 선언하기
  function* gen1() {
    // ...
  }

  // 표현식으로 사용하기
  const gen2 = function* () {
    // ...
  }

  // 메소드 문법으로 사용하기
  const obj = {
    * gen3() {
      // ...
    }
  }
  ```
  - 즉 Generator 함수를 호출하면 객체가 생성되는데, 이 객체는 Symbol.iterator 속성을 갖고 있다.
- Generator 함수 안에서는 `yield`라는 특별한 키워드를 사용할 수 있다. 이 키워드는 `return`과 유사한 역할을 하며, iterable 기능을 사용할때 `yield` 키워드 뒤에 있는 값들을 순서대로 넘겨준다.
  ```js
  function* numberGen() {
    yield 1;
    yield 2;
    yield 3;
  }

  // 1, 2, 3이 순서대로 출력됩니다.
  for (let n of numberGen()) {
    console.log(n);
  }
  ```

### 1-3. 클래스

#### ES2015 class
- ES2015에서 도입된 **클래스**는 생성자의 기능을 대체함
  ```js
    // 클래스
    class Person {
      // 이전에서 사용하던 생성자 함수는 클래스 안에 `constructor`라는 이름으로 정의합니다.
      constructor({name, age}) {
        this.name = name;
        this.age = age;
      }

      // 객체에서 메소드를 정의할 때 사용하던 문법을 그대로 사용하면, 메소드가 자동으로 `Person.prototype`에 저장됩니다.
      introduce() {
        return `안녕하세요, 제 이름은 ${this.name}입니다.`;
      }
    }

    const person = new Person({name: '윤아준', age: 19});
    console.log(person.introduce()); // 안녕하세요, 제 이름은 윤아준입니다.
    console.log(typeof Person); // function
    console.log(typeof Person.prototype.constructor); // function
    console.log(typeof Person.prototype.introduce); // function
    console.log(person instanceof Person); // true
  ```
  - 클래스는 함수로 호출될 수 없다.
  - 클래스 선언은 `let`과 `const`처럼 블록 스코프에 선언되며, 호이스팅이 일어나지 않는다.
  - 클래스의 메소드 안에서 `super` 키워드를 사용할 수 있다.

## 2. Today I found out
- es2015에 도입된 새로운기능들이 정말 많다고 다시한번 느끼게 되는 오늘 수업이었고 실무에서는 새로도입되는 기술들이 바로바로 적용되지는 않을것 같지만,쉴틈없이 변화하는 프론트엔드의 새로운 기술들은 항상 관심있게 볼 필요가 많은 것 같다.

## 3. Ref
- [redux-saga](https://github.com/redux-saga/redux-saga) -   Generator 관련 라이브러리