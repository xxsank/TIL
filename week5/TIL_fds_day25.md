# 4/20(금)

## 1. Today I learned

### 1-1. 함수형 프로그래밍

#### 고차함수
- 함수를 인수로 받는 함수, 함수를 반환하는 함수를 일러 **고차 함수** 라고 합니다.
  ```js
  // 함수를 인수로 받는 함수
  function func2(f) {
    f();
  }

  // 함수를 반환하는 함수
  function func1() {
    return function() {};
  }
  ```
  - 다른 함수의 인수로 넘겨지는 함수를 **콜백(callback)**이라고 부른다.
- 고차함수는 활용하는것이 어려움, 코드읽는것도 조금 어려워짐.
- 면접문제로 자주 나옴.

#### 클로저(Closure)
- 바깥 스코프에 있는 변수를 가져다 사용하는 함수와, 변수가 저장되는 저장소를 **클로저**라고 부른다.
  ```js
  function func1(x) {
  // 여기서 반환되는 함수는 바깥 스코프에 있는 변수 `x`를 사용하고 있습니다.
    return function () {
      return x;
    }
  }

  const func2 = func1(1);

  // `func1`의 실행은 끝났지만, `func2`를 통해서 변수 `x`를 사용할 수 있습니다.
  console.log(func2()); // 1
  ```

- 이같은 원리는 함수를 호출할때마다 스택과 힙이라는 메모리 저장공간과 연관이 있다.
- 클로저의 성질은 데이터를 숨기고 정해진 방법을 통해서만 데이터에 접근할 수 있도록 제한을 두는 데에도 활용된다.
  ```js
  function personFactory(initialAge) {
    let age = initialAge;
    return {
      getOlder() {
        age++;
      }
      getAge() {
        return age;
      }
    };
  }
  // `age`를 직접 변경할 수 있는 방법이 없습니다!
  ```

- 근래의 JavaScript 디버거는 클로저에 어떤 값이 들어있는지를 보여주는 기능을 포함하고있다.

#### 화살표 함수와 고차 함수
- 화살표 함수 문법을 이용하면, 적은 양의 코드를 사용해서 고차 함수를 만들 수 있다. 
- 간단한 고차 함수를 만들때는 화살표 함수를 써주는게 좋다.
  ```js
  const makeAdder = x => y => x + y;

  const add2 = makeAdder(2);
  add2(3); // 5
  
  makeAdder(2)(3); // 5 ,  이렇게도 가능함.
  ```

#### 재귀 함수 
- 함수 내부에서 자기 자신을 호출하는 함수를 재귀 함수라고 한다.
  ```js
  function func() {
  func();
  } 
  ```

- 루프를 재귀 함수로 재작성을 할 수 있다.
- 재귀호출을 사용하여 반복되는 루프를 짤 때 간결하게 쓸 수 있는 장점이있지만 되도록이면 일반루프로 작성하는게 좋다.

#### 분할 정복
- 분할 정복은 문제를 작운 부분 문제로 나누어서 푼 뒤, 그 결과를 합치는 식으로 알고리즘을 작성하는 기법이다. 재귀함수가 활용되는 대표적인 사례
- 분할 정복 기법을 활용하는 알고리즘 중 대표적인 예로 **병합 정렬(merge sort)**가 있다.
  ```js
  function mergeSort(arr) {
    // 입력된 배열의 길이가 1 이하이면 더 이상 재귀 호출을 하지 않습니다.
    if (arr.length <= 1) return arr;

    // 배열을 절반으로 잘라 두 개의 작은 배열로 분할하고,
    // 두 작은 배열에 대해 재귀 호출을 수행합니다.
    const slicer = Math.floor(arr.length / 2);
    const arr1 = mergeSort(arr.slice(0, slicer));
    const arr2 = mergeSort(arr.slice(slicer));

    // `arr1`, `arr2`는 **이미 정렬되어있는 상태**이므로,
    // 이 성질을 이용해 두 배열을 **정렬되어있는 큰 배열**로 합칠 수 있습니다.
    const newArr = [];
    for (let i = 0, j = 0; i < arr1.length || j < arr2.length; ) {
      if (arr1[i] == undefined || arr1[i] > arr2[j]) {
        newArr.push(arr2[j]);
        j++;
      } else {
        newArr.push(arr1[i]);
        i++;
      }
    }

    // 큰 배열을 반환합니다.
    return newArr;
  }
  ```

### 1-2. 객체 더 알아보기

#### 객체 자신의 속성
- 속성 접근자(property accessor)를 통해 객체의 속성에 접근할 때, 객체 자신이 갖고 있는 속성(own property)이 반환될 수도 있고, 혹은 프로토타입으로부터 상속받은 속성(inherited property)이 반환될 수도 있다.

#### 데이터 속성의 부수속성
- 자바스크리트에서는 각 속성마다 동작 방식이 다를 수 있다.
이에대한 정보는 속성의 부수속성이라고 불리는 곳에 숨겨져 있습니다.
- 부수속성을 알아보려면, `Object.getOwnPropertyDescriptor`라는 정적 메소드를 사용해 부수속성을 나타내는 객체를 얻을 수 있다. 이 객체를 속성 기술자(property descripto)라고 부른다.
  ```js
  const obj = {prop: 1};

  Object.getOwnPropertyDescriptor(obj, 'prop');
  // { value: 1, writable: true, enumerable: true, configurable: true }

  Object.getOwnPropertyDescriptor(Math, 'PI');
  // { value: 3.141592653589793, writable: false, enumerable: false, configurable: false }
  ```
  - `value` = 속성에 어떤 값이 저장되어 있는지를 나타냄.
  - `writable` = 변경할 수 있는 속성인지 나타냄.
  - `enumerable` = 열거 가능한 속성인지 나타냄.
  - `configurable` = 부수속성을 변경하거나 속성을 삭제할 수 있는지를 나타냄.

- 엄격 모드가 아닐 때 에는 `writable : false`, `configurable : false`인 속성을 변경하거나 삭제하려고 해도 에러가 나지 않고, 무시되지만, 엄격 모드일 때 에는 에러가 발생합니다.

#### 속성 기술자를 통해 객체의 속성 정의 하기
- 직접 속성 기술자를 이용해 속성을 정의할 수도 있다. 
  ```js
  const obj = Object.create(Object.prototype, {
  prop: {
      value: 1,
      writable: false,
      enumerable: true,
      configurable: false
    },
    another: {
      value: 2
    }
  });

  console.log(obj); // {prop: 1}

  obj.prop = 2;
  console.log(obj.prop); // 1

  delete obj.prop;
  console.log(obj.prop); // 1
  ```
  - 속성 기술자에 `writable`, `enumerable`, `configuralbe` 속성을 주지 않으면, 해당 부수속성은 모두 `false`로 취급된다.

- 속성 기술자를 인수로 받는 메소드
  - `Object.create`
  - `Object.defineProperty`
  - `Object.defineProperties`

#### 객체의 속성 열거하기
- 객체의 속성을 열거할 때에 사용할수 있는 방법
  - `Object.key` - **객체 자신의 속성** 중 열거 가능한 속성의 **이름**을 배열로 반환
  - `Object.values` - **객체 자신의 속성** 중 열거 가능한 속성의 **속성 값**을 배열로 반환
  - `Object.entries` - **객체 자신의 속성** 중 열거 가능한 속성의 **이름**과 **값**을 배열로 반환. 

#### 얕은 복사 & 깊은 복사
- `Object.assign` : 이 정적 메소드는 인수로 받은 객체들의 모든 열거 가능한 속성을 대상 객체에 복사한다.
  ```js
  const obj = {};
  Object.assign(obj, {a: 1}, {b: 2});

  console.log(obj); // { a: 1, b: 2 }
  ```
  - 대부분 위처럼 동작 하는 방식은 얕은 복사라고 하며 [clone](https://www.npmjs.com/package/clone) 라이브러리를 쓰면서 사용하면 깊은 복사라고 한다.

## 2. Today I found out

## 3. Ref