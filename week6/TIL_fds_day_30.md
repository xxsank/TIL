# 4/27(금)

## 1. Today I learned

### 1-1. 클래스

#### 메소드 정의하기
- 인스턴스 메소드 정의 하는 법
  ```js
  class Calculator {
    add(x, y) {
      return x + y;
    }
    subtract(x, y) {
      return x - y;
    }
  }
  ```

- 임의 표현식을 대괄호로 둘러싸서 메소드의 이름으로 사용할 수도 있다.
  ```js
  const methodName = 'introduce';
  class Person {
    constructor({name, age}) {
      this.name = name;
      this.age = age;
    }
    // 아래 메소드의 이름은 `introduce`가 됩니다.
    [methodName]() {
      return `안녕하세요, 제 이름은 ${this.name}입니다.`;
    }
  }

  console.log(new Person({name: '윤아준', age: 19}).introduce());
  ```

- **Getter**, **setter**를 정의하고 싶을 때 메소드 이름 앞에 `get`, `set`을 붙여 주면된다.
  ```js
  class Account {
    constructor() {
      this._balance = 0;
    }
    get balance() {
      return this._balance;
    }
    set balance(newBalance) {
      this._balance = newBalance;
    }
  }

  const account = new Account();
  account.balance = 10000;
  account.balance; // 10000
  ```

- `static` 키워드를 메소드 이름앞에 붙여주면 해당 메소드는 **정적 메소드**가 된다.
  ```js 
  class Person {
    constructor({name, age}) {
      this.name = name;
      this.age = age;
    }
    // 이 메소드는 정적 메소드입니다.
    static sumAge(...people) {
      return people.reduce((acc, person) => acc + person.age, 0);
    }
  }

  const person1 = new Person({name: '윤아준', age: 19});
  const person2 = new Person({name: '신하경', age: 20});

  Person.sumAge(person1, person2); // 39
  ```
  - 하나 정도의 작업을할때는 인스턴스 메소드
  - 여러개의 작업을 할 때는 정적 메소드
  - 하지만 선택의 차이일뿐. 

#### 클래스 필드
- 인스턴스 속성을 지정할 수 있는 문법 
  ```js
  class Counter {
    static initial = 0; // static class field
    count = Counter.initial; // class field
    inc() {
      return this.count++;
    }
  }

  const counter = new Counter();
  console.log(counter.inc()); // 0
  console.log(counter.inc()); // 1

  Counter.initial = 10;
  console.log(new Counter().count); // 10
  ```
  - 정식 표준으로 채택된 기능은 아님
  - Babel, TypeScript 등의 트랜스파일러를 통해 일부기능 사용가능

- 클래스 필드와 this
  - 화살표함수의 this는 바깥스코프의 this를 가르킨다.
    ```js
      class MyClass {
        a = 1;
        getA = () => {
          return this.a;
        }
      }

      new MyClass().getA(); // 1
    ```
  - 일반적인 메소드는 클래스의 `prototype`속성에 저장되는 반면, **클래스 필드**는 **인스턴스 객체에 저장된다**.
  - 화살표 함수의 `this`는 항상 인스턴스 객체를 가리킴.
  - 인스턴스 메소드를 다른함수의 인수로 넘길 때 function 문법함수를 사용하면 위험하고 화살표함수를 사용하면 `this`에 대한 걱정을 하지 않아도 된다.
  - **메소드를 값으로 다루어야 할 경우**에는 일반적인 메소드 대신 화살표 함수가 사용되는 경우가 종종 있다. 
  - 다만 클래스 필드를 통해 정의한 메소드는 **인스턴스를 생성할 때마다 새로 생성되기 떄문에** 메모리를 더 차지하게된다.

#### 클래스 상속
- 클래스 상속기능을 통해 한 클래스의 기능을 다른 클래스에서 **재사용**할 수 있다.
- 클래스 상속역시 기능의 재사용을 위한 것이다.
    ```js
    class Parent {
      // ...
    }

    class Child extends Parent {
      // ...
    }
    ```
  - `extends`키워드를 통해 `Child`클래스가 `Parent`클래스를 상속했다. 이관계를 부모 클래스 - 자식 클래스 관계 혹은 슈퍼 - 서브 관계라고 말한다.
    - 클래스 A가 클래스 B를 상속 받으면,
      - 자식 클래스 A를 통해 부모 클래스 B의 **정적 메소드와 정적 속성**을 사용할 수 있다.
      - 부모 클래스 B의 **인스턴스 메소드와 인스턴스 속성을** 자식 클래스 A의 인스턴스에서 사용할 수 있다.
      ```js
        class Parent {
          static staticProp = 'staticProp';
          static staticMethod() {
            return 'I\'m a static method.';
          }
          instanceProp = 'instanceProp';
          instanceMethod() { 
            return 'I\'m a instance method.';
          }
        }
        class Child extends Parent {}
        console.log(Child.staticProp);  // staticProp
        console.log(Child.staticMethod()); // I'm a static method.

        const c = new Child();
        console.log(c.instanceProp); // instanceProp
        console.log(c.instanceMethod()); // I'm a instance method.
      ```
- super
  ```js
  class Melon {
    getColor() {
      return '제 색깔은 초록색입니다.';
    }
  }

  class WaterMelon extends Melon {
    getColor() {
      return super.getColor() + ' 하지만 속은 빨강색입니다.';
    }
  }

  const waterMelon = new WaterMelon();
  waterMelon.getColor(); // 제 색깔은 초록색입니다. 하지만 속은 빨강색입니다.
  ```
  - `super` 키워드의 동작 방식
    - 생성자 내부에서 `super`를 함수처럼 호출하면, 부모 클래스의 생성자가 호출됩니다.
    - 정적 메소드 내부에서는 `super.prop`과 같이 써서 부모 클래스의 `prop` 정적 속성에 접근할 수 있습니다.
    - 인스턴스 메소드 내부에서는 `super.prop`과 같이 써서 부모 클래스의 `prop` 인스턴스 속성에 접근할 수 있습니다.

## 2. Today I found out

## 3. Ref