### 문제 1

두 수를 입력받아 큰 수를 반환하는 함수를 작성하세요.

- 정답

```js
function larger(x,y){
  // x가 y보다 크면
  if(x>y){
    // x를 반환.
    return x;
  }
  else{
    // 아니면 y를 반환
    return y;
  }
}
larger(10,20);
```

```js
function larger(x,y){
 return x > y ? x: y;
  }
}

larger(10,20);
```

### 문제 2

세 수를 입력받아 그 곱이 양수이면 `true`, 0 혹은 음수이면 `false`, 둘 다 아니면 에러를 발생시키는 함수를 작성하세요.

에러를 발생시키는 코드는 다음과 같습니다.

```js
throw new Error('입력값이 잘못되었습니다.');
```

- 정답
```js
function isPositive(x,y,z){
  if(x*y*z > 0){
    return true;
  }
  else if(x*y*z <= 0){
    return false;
  }
  else{
    throw new Error('입력값이 잘못되었습니다.');
  }
}
```

### 문제 3

세 수 `min`, `max`, `input`을 입력받아, 다음과 같이 동작하는 함수를 작성하세요.
- `min`보다 `input`이 작으면, `min`을 반환합니다.
- `max`보다 `input`이 크면, `max`를 반환합니다.
- 아니면 `input`을 반환합니다.

예:
```
limit(3, 7, 5); -> 5
limit(3, 7, 11); -> 7
limit(3, 7, 0); -> 3
```

- 정답

```js
function limit(min,max,input){
  if(min>input){
    return min;
  }
  else if(max<input){
    return max;
  }
  else{
    return input;
  }
}
```

### 문제 4

어떤 정수가 짝수인지 홀수인지 출력하는 함수를 작성하세요. 이를 이용해서, 1부터 20까지의 수가 각각 짝수인지 홀수인지 출력하는 프로그램을 작성하세요.

- 정답

```js
function evenOrOdd(){
  for(let i = 0;i<20;i++){
    if(i%2 === 1){
      console.log(`${i+1}은 짝수 입니다.`);
    }
    else{
      console.log(`${i+1}은 홀수 입니다.`);
    }
  }
}
evenOrOdd();
```

### 문제 5

100 이하의 자연수 중 3과 5의 공배수를 모두 출력하는 프로그램을 작성하세요.

- 정답

```js
function commonMult(){
  for(let i = 1;i<=100;i++){
    if(i%15 == 0){
      console.log(`${i}는 3과 5의 공배수 입니다.`);
    }
  }
}
commonMult();
```

### 문제 6

자연수를 입력받아, 그 수의 모든 약수를 출력하는 함수를 작성하세요.

```js
function divisor(x){
  for(i=1;i<x+1;i++){
    if(x%i === 0){
        console.log(x +` 의 약수는 ${x/i} 입니다.`);
    }
  }
}
```

### 문제 7

2 이상의 자연수를 입력받아, 그 수가 소수인지 아닌지를 판별하는 함수를 작성하세요.

- 정답
```js
function primeNum(x){
  let result = 0;
  if(x >= 2){
    for(let i=2;i<x+1;i++){
      if(x%i === 0){
        console.log('소수가 아닙니다.');
        break;
      }
      else{
        console.log('소수 입니다.');
        break;
      }
    }
  }
}
```

### 문제 8

1부터 100까지의 수를 차례대로 출력하되, 자릿수에 3, 6, 9중 하나라도 포함되어 있으면 '짝!'을 대신 출력하는 프로그램을 작성하세요.

- 정답

```js
for(let i = 1; i<=100; i++){
  const str = i.toString();
  if(str.includes('3') || str.includes('6') || str.includes('9')){
    console.log(`${i} 짝!`);
  }
  else{
    console.log(`${i}`)
  }
}
```

### 문제 9

양의 정수를 입력받아, 다음과 같은 패턴의 출력을 하는 함수를 작성하세요.

1을 입력받은 경우:
```
*
```

3을 입력받은 경우:
```
*
* *
* * *
```

5를 입력받은 경우:
```
*
* *
* * *
* * * *
* * * * *
```

- 정답

```js
function stair(n){
  let str = '';
  for(let i = 0; i < n; i++){
    console.log(str += '*');
  }
}
```

```js
// 이중 for문 
function stair(n){
  let str = '';
  for(let i=0 ;i<n; i++){
    for(let j=i; j<=i; j++){
      console.log(str += '* ');
    }
  }
}
```

```js
function stair(n){
  for(let i = 0; i<n;i++){
    let str = '';
    for(let j=0; j<i+1;j++){
      str += '* ';
    }
    console.log(str);
  }
}
```

### 문제 10

양의 정수를 입력받아, 다음과 같은 패턴의 출력을 하는 함수를 작성하세요.

1를 입력받은 경우:
```
*
```

3를 입력받은 경우:
```
  *
 * *
* * *
 * *
  *
```

5를 입력받은 경우:
```
    *
   * *
  * * *
 * * * *
* * * * *
 * * * *
  * * *
   * *
    *
```

- 정답

```js
function rhombus(n){
  for(let i = 0; i<n;i++){
      const str = ' '.repeat(n-i-1) + '* '.repeat(1+i) ;
      console.log(str);
  }
  for(let i = n-2; i>=0; i--){
      const str = ' '.repeat(n-i-1) + '* '.repeat(1+i) ;
      console.log(str);
  }
}
```

```js
// 코드중복 제거 위 코드 리팩토링
function line(n, i){
  const str = ' '.repeat(n-i-1) + '* '.repeat(1+i) ;
  console.log(str);
}

function rhombus(n){
  for(let i = 0; i<n;i++){
      line(n,i);
  }
  for(let i = n-2; i>=0; i--){
      line(n,i);
  }
}
```

```js
function line(n, i){
  const str = ' '.repeat(n-i-1) + '* '.repeat(1+i) ;
  console.log(str);
}

function rhombus(n){
  for(let i = 0; i<n;i++){
      line(n,i);
  }
  // 아래 for문 수정
  for(let i = 0; i < n-1 ; i++){
      line(n,n - i - 2);
  }
}
```

### 문제 11

두 수를 입력받아서, 두 수의 최대공약수를 반환하는 함수를 작성하세요. ([유클리드 호제법](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)을 참고하세요.)

### 문제 12

세 수를 입력받아 큰 것부터 차례대로 출력하는 함수를 작성하세요.

- 정답

```js
function sort(x,y,z){
  //셋 중에 제일 큰 놈을 따로 빼기
  let large = x > y ? x : y;
  let small1 = x > y ? y : x;
  let max = large > z ? large : z;
  let small2 = large > z ? z : large;
  if(small1>small2){
    return console.log(max,small1,small2);
  }
  if(small1<small2){
    return console.log(max,small2,small1);
  }
}
```
### 문제 13

자연수 `n`을 입력받아, `n`번째 피보나치 수를 반환하는 함수를 작성하세요.