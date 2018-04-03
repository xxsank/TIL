# 4/02(월)

## 1. Today I learned

### 1-1. html/css

#### 1-1-1 웹 접근성
  - 링크 텍스트
    - 링크 텍스트는 용도나 목적을 이해할 수 있도록 제공해야 한다.
    - 링크 텍스트를 "여기를 클릭하세요", "여기"와 같은 애매모호한 표현을 사용하면 시각장애인이나 인지장애 뿐만 아니라 비장애인들도 링크를 클릭했을 때 어떤 반응이나 어떤 페이지로 이동될 지 예측하기 어려움.
    - 구체적인 더보기 링크 제공을 해당 링크의 목적지에 대한 정보가 확실하게 표현하는게 좋다.
    - 링크의 목적이나 용도를 이해할 수 있도록 정보를 제공해 주는것이 링크 텍스트 사용의 핵심.

#### 1-1-2 calc() functionss
  - calc()
    - calc()함수는 width,height,font-size,margin,padding 값의 길이를 계산할때나 각도, 수치, 변형, 사운드 재생 횟수, 애니메이션 처리시 사용하는 함수이다. 이를 표현하기 위해선 더하기, 빼기, 곱하기, 나누기등 사칙연산자를 이용하여 표현할수 있다.  
    ex)  
      ```css
      div {
      height: calc(100% - 50px);
      padding-left: calc(100% - 50px);
      }
      ```
      - 보통 위와 같이 표현하게되며 사칙연산자 앞,뒤에는 항상 공백이 들어가야 한다.

#### 1-1-3 white-space 속성
  - white-space
    - `white-space` 속성은 내부에서의 자동 줄 바꿈 여부를 나타내는 값을 설정한다.

    - 속성값 

      속성 | 설명
      -----|-----
      normal |  기본값으로 글자 줄이 자동으로 바뀐다. 콘텐츠가 요소의 너비를 초과할 경우 다음줄로 바뀜, 기본값.
      nowrap | 줄 바꿈이 실행 되지않는다. 콘텐츠가 다음 줄로 바뀌지 않음.
      pre | 줄 바꿈과 기타 공백이 유지된다. 공백을 코드에 있는 그대로 표시함
      pre-line | 공백을 여러개 넣어도 1개만 표시, 코드에 줄바꿈이 없어도 자동 줄바꿈이 되며, 줄바꿈이 있을 때도 그대로 표시한다.
      pre-wrap | 공백을 코드에 있는 그대로 표시, 코드에 줄바꿈이 없어도 자동 줄바꿈이 된다.
    
    - 예제)

      ```html
      <!-- html 코드 -->
      <p> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
  
      Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
  
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
      ```

      - white-space:normal
        ```css
        p{
        white-space: normal;
        }
        ```
        ![inline](/week3/images/normal.PNG) 
      
      - white-space:nowrap
        ```css
        p{
        white-space: nowrap;
        }
        ```
        ![inline](/week3/images/nowrap.PNG) 

      - white-space:pre
        ```css
        p{
        white-space: pre;
        }
        ```
        ![inline](/week3/images/pre.PNG) 

      - white-space:pre-line
        ```css
        p{
        white-space: pre-line;
        }
        ```
        ![inline](/week3/images/pre-line.PNG) 

      - white-space:pre-wrap
        ```css
        p{
        white-space: pre-wrap;
        }
        ```
        ![inline](/week3/images/pre-wrap.PNG) 

#### 1-1-4 text-overflow 속성
  - text-overflow
    - `text-overflow` 는 박스 안에 내용이 넘칠 때 텍스트를 어떻게 처리할지 지정 하는 속성이다. 게시판등과 같에 어떤 텍스트가 있을 때 ...기호를 사용하여 추가적으로 더 많은 글이 있다는 것을 쉽게 알 수 있게 하는것이다.

    - 이 속성을 만족 시키려면  
    ```
    1. overflow: 속성 값이 hidden,scroll,atuo 일때
    2. white-space:nowrap 또는 텍스트가 다음 줄로 이동하지 않는 경우.
    ```

    - 속성 값

      속성 | 설명
      -----|-----
      clip | 텍스트를 잘라낸다.
      ellipsis | 텍스트가 잘렸다는 것을 표현하기 위해 말줄임표(...)를 표시한다.

    - 예제)
      - text-overflow: clip
        ```css
        p{
        white-space: nowrap;
        overflow: hidden;
        text-overflow: clip;
        }
        ```
        ![inline](/week3/images/clip.PNG) 

       - text-overflow: ellipsis
         ```css
         p{
         white-space: nowrap;
         overflow: hidden;
         text-overflow: ellipsis;
         }
         ```
          ![inline](/week3/images/ellipsis.PNG) 


## 2. Today I found out
  - float 속성을 이용한 레이아웃 배치가 전보단 훨씬 눈에 더 잘들어오고 이해가 많이 되었다.  

## 3. Ref
[Webdir](http://webdir.tistory.com/347)