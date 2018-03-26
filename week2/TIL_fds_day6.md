# 3/26(월)

## 1. Today I learned

### 1-1. html
- 목록을 만드는 태그

  - `<ul>` : Unoerdered List 의 약자로 순서가 없는, 정렬되지 않는 목록을 만들때 사용 하는 태그이다.글머리 기호를 붙혀서 목록을 만드는 형식이다.  `<li>` 태그와 함께 사용 한다.
  - `<li>` : List Item 의 약자 이며 단독으로 쓰이지 않는다. `<ul>` 혹은 `<ol>`태그 내부에 들어간다. 단순히 리스트 나열 뿐만이 아니라 메뉴 등을 만들때도 사용한다.

  *ex*)
  ```html
  <ul class="과일">     
    <ls>사과</ls>
    <ls>포도</ls>
  </ul>
  ```
- 문서를 연결하는 태그
  
  - `<a>` : 하이퍼 링크를 정의 하는 내용으로 링크를 통해 다른 웹페이지로 이동하거나, 문서 내에서도 이동이 가능하다. 어떤 상황이나 조건이 맞아야 들어감.
  - `<href>` : 위와같은 `<a>`태그와 함께 쓰는 명령어로 링크의 목적지 이동 url을 나타낸다. `<href>`가 없으면 interactive model이 아니다.

  *ex*)
  ```html
  <a href="http://facebook.com">페이스북</a>
  ```



   

### 1-2. css
- Normalize
  - 브라우저를 광범위하게 지원하며, HTML5요소, 타이포그래피, 목록(list), 폼과 테이블을 일관성있게 통일시키는 CSS를 포함한다. 초기화 시키는 Reset과 비슷 하지만 어느정도 스타일이 가미되어있다.
  브라우저의 **오차**를 줄이기 위해 연동시켜 사용하며 현재는 8.0버전이 최신버전.
    - 사용방법 
      ```css
       @import url("normalize.css"); 
       /* normalize.css 파일을 생성했을 경우 */
       @import url("https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.0/normalize.css"); 
       /* 주소를 직접 참조해서 사용할 경우 */
      ```
- Reset
  - Reset이란 설명하자면 브라우저간의 오차를 최대한 없애서(예를 들어 브라우저들이 갖고 있는 기본 글꼴등), 스타일이 0인 상태에서 디자인을 만들어 나가기 위해 생겨난것이다. 쉽게 말해 **초기화**  마찬가지로 현재는 2.0버전이 아직까지 최신버전이다.
    - 사용방법은 위와 동일.

- css web font
  - 기본 시스템 폰트가 아닌 일반 사용자 폰트로 웹을 표시해주는 것을 웹폰트 적용한다라고 말한다. 글꼴방식은 다양한 사용자들을 위해 항상 고려해야하며 마지막엔 항상 글꼴군을 선언해 주어야한다.
  ```css
  @import url('http://fonts.googleapis.com/earlyaccess/nanumgothic.css');
  /* google font service를 이용한 CDN방식 */
  font-family: 'Noto Sans Regular', sans-serif;
  /* 마지막엔 글꼴 군 선언 */
  ```
- css 상속이란?
  - 기본적으로 CSS 속성은 상속하는 속성과 상속하지 않는 속성이 있다. 상속하는 속성은 자식 요소에 영향을 미치며, 상속하지 않는 속성은 자식 요소에 미치지 않는다. 기본적인 css스타일은 상속처리가 된다. 허나 모든 css 속성들이 상속되는 것은 아니다.

- float 속성
  - float을 그대로 번역하면 일단 ` `띄우다` `라는 뜻이다. 
  
    ~~C,C++,JAVA등의 float(부동소수점 방식의 실수형)과 완전 다르다..~~
    
    느낌대로 float 레이아웃은 이미지나 콘텐츠등을 띄우는 느낌을(?) 강하게 준다. 부모를 기준으로 left 또는 right에 배치 시킬수 있으며,
    
    



## 2. Today I found out


