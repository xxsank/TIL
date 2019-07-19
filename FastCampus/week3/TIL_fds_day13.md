# 4/04(수)

## 1. Today I learned

### 1-1. html
  
#### 1-1-1. 인용문 관련 태그
  - q : - 짧은 인용문 사용시 넣는 태그이다, 자동으로 따옴표("")를 붙여 출력하며 출처가 명확할 경우 `cite=""`속성을 사용할 수 있다. 인라인 태그로 줄 바꿈 없이 한 줄에 표시된다.

  - blockquote : q태그와 성격이 비슷하나 `blockquote` 태그는 block요소 태그로 줄바꿈과 들여쓰기가 되어 표시됨.

    예제)

    ```html
    <q cite="http://w3.org/WAI">
    The power of the Web is in its universality, Access by everyone reg
    ardless of disability is an essential aspect.</q>

    <blockquote cite="http://w3.org/WAI">
    The power of the Web is in its universality, Access by everyone reg
    ardless of disability is an essential aspect.</blockquote>
    ```
    ![inline](/week3/images/qtag.PNG) 

#### 1-1-3. 특수문자 태그 표
  - html 상에서 특수문자가 제대로 나타지 않을 수 있기 때문에 특수문자를 숫자나,문자로 사용해서 표현할 수 있다.

    종류가 너무 많으므로 구글이나 W3 레퍼런스에서 찾아보자.
    [W3schools Symbols Reference](https://www.w3schools.com/charsets/ref_utf_symbols.asp) 


### 2-1. css

#### 2-1-1. 구조선택자
  - 구조 선택은 구조상 같은 위치의 태그를 선택하는 태그이다.

  선택자 형태 | 설명
  ----- | -----
  :first-child | 형제 관계 첫번째에 위치하는 태그를 선택
  :last-child | 형제 관계 중에서 마지막에 위치하는 태그를 선택
  :nth-child(수열) | 앞에서 수열 번째에 있는 태그를 선택
  :nth-last-child(수열) | 뒤에서 수열 번째에 있는 태그를 선택

#### 2-1-2. content
  - `content` 속성은 `:before`,'`:after` 가상 요소와 주로 같이 쓰이며 html문서에 쓰지 않고도 css로 내용을 생성 하는 역할을 한다.

  속성값 | 설명
  ----- | -----
  normal | 기본값으로 아무것도 표시하지 않음
  none | attr(속성) 해당 속성의 속성값을 표시한다.
  string | " " 사이에 문자열을 집어넣어서 `content:"문자열"`과 같이 사용한다.
  url | 외부 자원(사진, 비디오 등)을 표시한다.
  count | 순서를 차례대로 생성하며 `counter-increment`과 `counter-reset`속성과 함께 사용한다. 리스트의 기능과 비슷

  - counter-increment : `counter-increment`는 값을 증가 시키는 역할을 한다.

  - 문법
    ```css
    .favorite-site-list li{
      counter-increment: number;
    }  
    .favorite-site-list li::before{
      content: counter(number, decimal);
    }
    ```

## 2. Today I found out
  - 약 2주간의 걸쳐 정말 많은걸 배우면서 하나의 웹페이지를 구성했다. 아직은 쉽지 않지만 계속 구조를 뜯어보고 주석다는 연습을 익숙하게 해봐야 겠다는 생각이 든다. 항상 웹접근성 관점으로 생각하고 그리는 연습을 해봐야겠다.

## 3. Ref
  - [nthmaster](http://nthmaster.com/)
  - [W3schools Symbols Reference](https://www.w3schools.com/charsets/ref_utf_symbols.asp)