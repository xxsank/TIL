### 문제 1

두 문자열을 입력받아, 대소문자를 구분하지 않고(case insensitive) 두 문자열이 동일한지를 반환하는 함수를 작성하세요.

예:
```
insensitiveEqual('hello', 'hello'); -> true
insensitiveEqual('hello', 'Hello'); -> true
insensitiveEqual('hello', 'world'); -> false
```

```js
// if문 사용
function string(x,y){
  let str1,str2;
  str1 = x.toLowerCase();
  str2 = y.toLowerCase();
  
  if(str1 === str2){
    return true;
  }
  else
    return false;
}
```

```js
// 3항연산자 사용
function string(x,y){
  let str1,str2;
  str1 = x.toLowerCase();
  str2 = y.toLowerCase();
  return str1 === str2 ? true : false;
}
```

### 문제 2

문자열 `s`와 자연수 `n`을 입력받아, 만약 `s`의 길이가 `n`보다 작으면 `s`의 왼쪽에 공백으로 추가해서 길이가 `n`이 되게 만든 후 반환하고, 아니면 `s`를 그대로 반환하는 함수를 작성해보세요.

예:
```
leftPad('hello', 8); -> '   hello'
leftPad('hello', 3); -> 'hello'
```
- 정답

```js
function leftPad(str, num) {
  if (str.length < num) {
    // 공백 추가 후 반환
    const spaceLength = num - str.length;
    return ' '.repeat(spaceLength) + str;
    // 과제: for 루프 써서 해보기!
  } else {
    return str;
  }
}
```

### 문제 3

문자열을 입력받아, 문자열 안에 들어있는 모든 모음(a, e, i, o, u)의 갯수를 반환하는 함수를 작성하세요.

- 정답

```js
function countVowel(str){
 let count = 0;
 
 for(let i=0;i<str.length;i++){
    if(
      str[i] === 'a' || 
      str[i] === 'e' || 
      str[i] === 'i' || 
      str[i] === 'o' || 
      str[i] === 'u'
      ) {
      count++;
    }
 }
 return count;
}
```

### 문제 4

문자열을 입력받아, 해당 문자열에 포함된 문자의 종류와 갯수를 나타내는 객체를 반환하는 함수를 작성하세요.

예:
```
countChar('tomato'); -> {t: 2, o: 2, m: 1, a: 1}
```

- 정답

```js
// ### 문제 4

// 문자열을 입력받아, 해당 문자열에 포함된 문자의 종류와 갯수를 나타내는 객체를 반환하는 함수를 작성하세요.

// 예:
// ```
// countChar('tomato'); -> {t: 2, o: 2, m: 1, a: 1}
// ```

function countChar(str) {
  const obj = {};
  for (let i = 0; i < str.length; i++) {
    const char = str[i];
    // 만약 속성이 없다면
    if (obj[char] == null) { // null check
      // 속성 값에 1 저장
      obj[char] = 1;
    } else {
      // 속성이 있으면 1 증가
      obj[char]++;
    }
  }
  return obj;
}

// 식별자 이름이 아닌 속성 이름을 사용할 때에는 반드시 대문자 표기법을 사용해야 한다.
// 변수에 대입되어 있는 문자열과 같은 이름의 속성을 가져올 때도 반드시 대문자 표기법을 사용해야 한다.

// > const obj = {a: 1, b: 2}
// => undefined
// > obj.a
// => 1
// > obj['a']
// => 1
// > const propName = 'a'
// => undefined
// > obj[propName]
// => 1
```

### 문제 5

문자열을 입력받아 그 문자열이 회문(palindrome)인지 판별하는 함수를 작성하세요. (회문이란, '토마토', 'never odd or even'과 같이 뒤에서부터 읽어도 똑같이 읽히는 문자열을 말합니다.)

- 정답

```js
function isPalindrome(str){
  // 처음과 마지막부터 시작해 전체를 탐색
 for(let i=0;i<str.length;i++){
   // str[i]번째가 뒤에서 부터 시작되는 str[str.length-i-1]번째와 같지 않다면
  if(str[i] !== str[str.length -i -1]){
    // false 반환
    return false;
  }
 }
 //true 반환
 return true;
}
```

```js
function isPalindrome(str){
  // 문장의 가운데까지 확인
 for(let i=0; i< Math.floor(str.length / 2);i++){
  if(str[i] !== str[str.length -i -1]){
    return false;
  }
 }
 return true;
}
```

### 문제 6

문자열을 입력받아, 그 문자열의 모든 '부분 문자열'로 이루어진 배열을 반환하는 함수를 작성하세요.

예:
```
subString('햄버거');
// 결과: ['햄', '햄버', '햄버거', '버', '버거', '거']
```

- 정답
```js
function subString(str){
  // 결과값을 받을 새로운 배열을 추가한다.
  const arr = [];
  for(i=0;i<str.length;i++){
    // 문자열 첫번째부터 순차적으로 탐색하기위해 for문을 추가 선언
    for(j=i;j<str.length;j++){
      // 새로만든 배열에 i번째부터 j+1번째를 slice한 값을 push 한다.
      arr.push(str.slice(i,j+1));
    }
  }
  return arr;
}
```

### 문제 7

문자열을 입력받아, 해당 문자열에서 중복된 문자가 제거된 새로운 문자열을 반환하는 함수를 작성하세요.

예:
```
removeDuplicates('tomato'); -> 'toma'
removeDuplicates('bartender'); -> 'bartend'
```

- 정답
```js
function removeDuplicates(str) {
  let newStr = '';
  for(let i =0;i < str.length; i++){
    if(!newStr.includes(str[i])){
      newStr += str[i];
    }
  }
  return newStr;
}
```

### 문제 8

이메일 주소를 입력받아, 아이디 부분을 별표(`*`)로 가린 새 문자열을 반환하는 함수를 작성하세요.

- 루프로 먼저 풀어보세요.
- `split` 메소드를 이용해서 풀어보세요.

- 정답

```js
function email(str){
  let pos;
  for(let i=0;i<str.length;i++){
    if(str[i] === ('@')){
      pos = i;
      break;
    }
  }
  const afterAt = str.slice(pos,str.length);
  const stars = '*'.repeat(pos);
  return stars + afterAt ;
}

function email(str){
  const pos = str.indexOf('@');
  const afterAt = str.slice(pos,str.length);
  const stars = '*'.repeat(pos);
  return stars + afterAt;
}

function email(str){
  const arr = str.split('@');
  console.log(arr);
  stars = '*'.repeat(arr[0].length);
  const afterAt = arr[1];
  return stars + '@' + afterAt;
}
```

### 문제 9

문자열을 입력받아, 대문자는 소문자로, 소문자는 대문자로 바꾼 결과를 반환하는 함수를 작성하세요.

- 정답
```js
function swapCase(str) {
	let newStr = '';

	for (let i = 0; i < str.length; i++) {
		if (str[i].toLowerCase() === str[i]) {
			newStr += str[i].toUpperCase();
		} else {
			newStr += str[i].toLowerCase();
		}
	}
	
	return newStr;
}
```

### 문제 10

문자열을 입력받아, 각 단어의 첫 글자를 대문자로 바꾼 결과를 반환하는 함수를 작성하세요. (문자열에 개행이 없다고 가정합니다.)

- 정답

```js
function capitalize(str){
  let newStr = '';
  for(let i=0; i<str.length; i++){
    if(str[i-1] === ' ' || i === 0){
      newStr += str[i].toUpperCase();
    }
    else{
      newStr += str[i];
    }
  }  
  return newStr;
}
```

### 문제 11

문자열을 입력받아, 문자열 안에 들어있는 단어 중 가장 긴 단어를 반환하는 함수를 작성하세요. (문자열에 개행이 없다고 가정합니다.)

- 정답

```js
function maxLength(str){
  let currentLen = 0;
  let maxLen = 0;
  for(let i=0;i<str.length;i++){
    if(str[i] === ' '){
      maxLen = maxLen>currentLen ? maxLen : currentLen;
      currentLen = 0;
    }
    else{
      currentLen++;
    }
  }
  return maxLen > currentLen ? maxLen : currentLen;
}
```

```js
function maxLength(str){
  const words = str.split(' ');
  let maxLen = 0;
  for (let i =0; i < words.length;i++){
    maxLen = words[i].length > maxLen ? words[i].length : maxLen;
  }
  
  return maxLen;
}
```

### 문제 12

문자열 `s`과 자연수 `n`을 입력받아, `s`의 첫 `n`개의 문자만으로 이루어진 새 문자열을 반환하는 함수를 작성하세요.

- 정답

  ```js
  function firstStr(s,n){
  let val = '';
  for(let i = 0; i<s.length;i++){
    if(i === n){
      val = s.slice(0,i);
    }
  }
  return val;
  }
  ```

  ```js
  function firstStr(s,n){
  let val = '';
  for(let i = 0; i<s.length && i<n ;i++){
    val += s[i]
  }
  return val;
  }
  ```

  ```js
  function firstStr(s,n){
   return  Array
    .from(s)
    .filter((item,index) => index < n)
    .join('');
  }
  ```

- 힌트
  // slice
  // filter join

### 문제 13

Camel case의 문자열을 입력받아, snake case로 바꾼 새 문자열을 반환하는 함수를 작성하세요.

- 정답

  ```js
  function camelToSnake(str){
  let snake = '';
  
  for(let i = 0; i<str.length; i++){
    if(str[i].toUpperCase() === str[i]){
      if(str[i] === str[0]){
        snake += str[i].toLowerCase();
      }else{
      snake += '_' + str[i].toLowerCase();
      }
    }
    else
      snake += str[i].toLowerCase();
  }
  return snake;
  }

  camelToSnake('HelloWorldJavaScript');
  ```

  ```js
  function camelToSnake(str){
  return str.replace(/([A-Z])/g, match => '_' + match[0].toLowerCase());
  }
  ```

### 문제 14

Snake case의 문자열을 입력받아, camel case로 바꾼 새 문자열을 반환하는 함수를 작성하세요.

- 정답

```js
function snakeToCamel(str){

  let val = '';
  
  
  for(let i = 0; i<str.length; i++){
    if(str[i] === str[0]){ val += str[i].toUpperCase(); i++}
    if(str[i] !== '_') val += str[i];
    else{val += str[i+1].toUpperCase(); i++;}
  }
  return val;
}
snakeToCamel('hello_world_java_script');
```

### 문제 15

`String.prototype.split`과 똑같이 동작하는 함수를 작성하세요.

예:
```
split('Hello World'); -> ['Hello World']
split('Hello World', ' '); -> ['Hello', 'World']
split('let,const,var', ',') -> ['let', 'const', 'var']
```

- 정답
  
  ```js
  function split(str, sep){
  const arr = [];
  let val = '';

  for(let i=0; i<str.length; i++){
      val += str[i];
    if(str[i] === sep){
      // replace('찾을문자열','바꿀문자열')
      // 바꿀문자열에 빈문자열을 넣으면 찾을문자열만 없어진다
      val = val.replace(',','');
      arr.push(val);
      val = '';
    }
  }
    arr.push(val);
    return arr;
  }
    
  split('let,const,var', ',');
  ```

  ```js
  function split(str, sep){
  const arr = [];
  let currentWord = '';
  for(let i=0; i<str.length; i++){
    if(str[i] === sep){
      arr.push(currentWord);
      currentWord = '';
    } else{
        currentWord += str[i];
    }
  }
  arr.push(currentWord);
  return arr;
  }

  split('let,const,var',',')
```

### 문제 16

2진수를 표현하는 문자열을 입력받아, 그 문자열이 나타내는 수 타입의 값을 반환하는 함수를 작성하세요. (`parseInt`를 사용하지 말고 작성해보세요.)

예:
```
convertBinary('1101'); -> 13
```

- 정답

  ```js
  function convertBinary(str){
    // 하나씩 계산하기 위해 배열 선언
    const arr = [...str];
    // for문으로 2^n계산을 쉽게하기 위해 revers로 뒤집어줌
    arr.reverse();
    // 더한값을 저장해주기 위한 변수 선언;
    let num = 0;
  
    for(let i=0; i<arr.length;i++){
      if(arr[i] === '0'){
        num += 0;
      }
      else{
        num += 2**i;
      }
    }
    return num;
  }

  convertBinary('1111');
  ```

  ```js
  function convertBinary(str){
  let num = 0;
  for(let i=0; i<str.length; i++){
    if(str[str.length - i - 1] === '1'){
      num += 2 ** i;
    }
  }
  return num;
  }
  ```

### 문제 17

숫자로만 이루어진 문자열을 입력받아, 연속된 두 짝수 사이에 하이픈(-)을 끼워넣은 문자열을 반환하는 함수를 작성하세요.

예:
```
insertHyphen('437027423'); -> '4370-274-23'
```

- 정답

  ```js
  function insertHyphen(num){
    let number = '';
    
    for(let i=0; i<num.length; i++){
      number += num[i];
      if((num[i]%2 === 0) && (num[i+1]%2 === 0)){
        number += '-';
      }
    }
    return number;
  }

  insertHyphen('437027423');
  ```