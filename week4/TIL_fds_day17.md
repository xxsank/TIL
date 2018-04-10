# 4/09(월)

## 1. Today I learned

### 1-1. string type

#### string type 
- string type은 문자열 이라고 부르며, string 타입을 통행 일반적인 텍스트 데이터를 다룰 수 있습니다.

#### 템플릿 리터럴
- ES2015에서 도입된 템플릿 리터럴은 문자열 리터럴의 일종으로, 추가적인 기능을 지원한다. 템플릿 리터럴을 사용하려면 backtick(`)로 문자열을 둘러 싸준다.

  ```js
  const str1 = `hello` // template literal
  const str2 = `world` // template literal
  // 이런식으로 문자열을 동적으로 생성하는 코드를 작성할 수 도 있다.
  const sentence = `${str1} ${str2}!`; 
  ```

#### 문자열과 연산자
- 수 타입 뿐 아니라 문자열에 대해서도 여러 가지 연산자를 쓸 수 있습니다.

  ```js
   // 문자열 연결하기
  'hello' + 'world'; // 'helloworld'

  // 등호 비교
  'hello' === 'hello'; // true
  'hello' !== 'hello'; // false

  // 유니코드 코드포인트 비교. 앞에서부터 한 글자씩 차례대로 비교합니다.
  'a' < 'b'; // true
  'aaa' < 'abc'; // true
  'a' < 'Z'; // false
  '한글' < '한국어'; // false
  '2' < '10'; // false

  // 문자열을 배열로 바꾸기
  [...'hello']; // ['h', 'e', 'l', 'l', 'o']
  ```

#### 속성 및 메소드
- string 타입도 래퍼 객체의 속성과 메소드를 사용할 수 있다.

  ```js
  // 문자열의 길이 알아내기
  'hello'.length; // 5

  // 여러 문자열 연결하기
  'hello'.concat('fun', 'javascript'); // 'hellofunjavascript'

  // 특정 문자열을 반복하는 새 문자열 생성하기
  '*'.repeat(3); // '***'

  // 특정 문자열이 포함되어 있는지 확인하기
  'hello javascript'.includes('hello'); // true
  'hello javascript'.startsWith('he'); // true
  'hello javascript'.endsWith('ript'); // true
  'hello javascript'.search('java'); // 6

  // 문자열의 특정 부분을 바꾼 새 문자열 생성하기
  'hello javascript'.replace('java', 'type'); // 'hello typescript'

  // 문자열의 일부를 잘라낸 새 문자열 생성하기
  'hello'.slice(2, 4); // 'll'

  // 좌우 공백문자를 제거한 새 문자열 생성하기
  '   hello  '.trim(); // 'hello'
  '   hello  '.trimLeft(); // 'hello  '
  '   hello  '.trimRight(); // '   hello'

  // 좌우 공백문자를 추가한 새 문자열 생성하기
  'hello'.padStart(8); // '   hello'
  'hello'.padEnd(8); // 'hello   '

  // 문자열을 특정 문자를 기준으로 잘라 새 배열 생성하기
  'hello!fun!javavscript'.split('!'); // ['hello', 'fun', 'javascript']
  'hello'.split(''); // ['h', 'e', 'l', 'l', 'o']

  // 모든 문자를 소문자, 혹은 대문자로 변환한 새 문자열 생성하기
  'Hello JavaScript'.toLowerCase(); // 'hello javascript'
  'Hello JavaScript'.toUpperCase(); // 'HELLO JAVASCRIPT'
  ```

### 1-2. boolean type

#### boolean type
- boolean 타입에 해당하는 값은 `true`,`false` 두 가지 밖에 없다. 이 값들을 진리값이라고 부른다.
  ```js
  1 < 2; // true
  1 > 2; // false
  3 === 3; // true
  3 !== 3; // false
  Number.isFinite(Infinity); // false
  Number.isNaN(NaN); // true
  'hello'.includes('ll'); // true
  ```

#### truthy & falsy
- JavaScript 에서는 boolean 타입이 와야 하는 자리에 다른 타입의 값이 와도 에러가 나지 않고 실행된다. 이렇게 어떤 값들은 `true`로, 어떤 값들은 `false`로 취급되는데 전자를 **truthy**, 후자를 **falsy**라 부른다
  
  - `false`
  - `null`
  - `undefined`
  - `0`
  - `NaN`
  - `''`

  위 값들은 모두 **falsy**이고, 이를 제외한 모든 값들은 **truthy**입니다.
### 1-3. null과 undefined

#### null과 undefined
- JavaScript에는 `없음`을 나타내는 값이 두 개가 있는데, 바로 `null`과 `undefined`이다. 두 값의 의미는 비슷하며 각각 사용되는 목적은 다르다.

  ```js
  // 값이 대입되지 않은 변수 혹은 속성을 사용 하려하면 undefined를 반환한다.
  let foo;
  foo // undefined

  const obj = {};
  obj.prop; // undefined
  ```

- `null`은 객체가 없음을 나타낸다.

  ```js
  typeof null // 'object'
  typeof undefined // 'undefined'
  ```

- 프로그래머 입장에서 명시적으로 부재를 나타내고 싶다면 항상 `null`을 사용 하는것이 좋다.

- 다만 객체를 사용할 때 어떤 속성의 부재를 `null`을 통해서 나타내는 쪽보다는, 그냥 그 속성을 정의하지 않는 방식이 더 간편하므로 더 널리 사용된다.

  ```js
  // 이렇게 하는 경우는 많지 않다.
  {
    name: 'Seungha',
    address: null
  }

  // 일반적인 경우.
  {
    name: 'Seungha'
  }

  // 해서는 안될 경우.
  {
    name: 'Seungha',
    address: undefined
  }
  ```

#### Null Check
- `null`이나 `undefined`는 어떤 변수에도, 어떤 속성에도 들어있을 수 있기 때문에, 어떤 값이 `null`혹은 `undefined`인지 확인하는 작업을 `null check`라고 한다.  

- null check를 할 때 만큼은 `==` 를 쓰는 것이 편리하다. 그렇지 않은 다른 모든 경우에서는 `===`를 사용하는 것이 좋다.

  ```js
  null === undefined; // false
  null == undefined;  // true

  null == 1       // false
  null == 'hello' // false
  null == false   // false

  undefined == 1       // false
  undefined == 'hello' // false
  undefined == false   // false
  ```

  - `==`연산자는 즉 한 쪽 피 연산자에 `null`이나 `undefined`가 오면 다른 쪽 피 연산자에 `null`,`undefined`가 왔을 때만 `true`를 반환하고, 다른 모든 경우에는 `false`를 반환한다.

## 2. Today I found out
- truthy,falsy라는 개념이 있다는게 조금 낯설었지만 공부를 더해서 완전히 이해 해야겠다는 생각이 든다. 자바스크립트는 언제나 새로운 것 같다. 

## 3. Ref
