# 4/02(월)

## 1. Today I learned

### 1-1. html/css
  - form
    - 폼은 웹 페이지의 정보를 다른 페이지로 전송하는 역할을한다. 입력된 데이터를 한번에 서버로 전송하며, 내용만 보여주는 페이지에는 필요 없지만 데이터를 주고 받고 움직일때는 반드시 들어가는 요소이다. 주로 회원가입이나 로그인 등 사용자의 입력을 필요로 할때 사용된다.

    - input 태그 
      - input태그란 form 태그안에서 추가 입력되는 요소들 중 가장 중요한 태긔다. 사용자로부터 정보를 받아들이는 용도로 사용되며 type이라는 속성을 이용해 입렬 양식을 여러가지로 변경해서 사용하기도 한다.  
      ex)
      ```html
      <input type="text" id="user-name" required placeholder="예) 홍길동">
      ```

      - type 속성  

       속성값|설명
       ----- | -----
       text | - 텍스트를 입력하는 창을 생성한다.</br>- 아이디, 이름, 주소와 같은 텍스트를 입력할 때 사용
       password | - 비밀번호를 입력하는 창을 생성한다.</br>- 텍스트 필드와 같지만, 입력하는 내용에 `*`로 표시가 됨
       checkbox | - 여러 항목중에서 2개 이상 선택할 수 있는 체크박스를 정의
       radio | - 여러 개의 항목 중에서 한 가지만 선택하도록 하는 버튼을 정의.</br>- 이미 선택된 항목이 있을 때 다른 항목을 선택하면 취소가 된다.
       file | - 파일을 첨부 하려고 할 때 사용하며 파일이 여러개 선택하는걸 허용한다
       submit | - 폼에 입력한 정보를 서버로 전송하는 submit 버튼 표시.</br>- submit 버튼으로 전송된 정보는 처음에 <form>태그에서 지정한 위치로 전송
       button | - 폼 안에 버튼 형태를 만듦
       url | - URL 입력을 위한 필드 정의
       email | - 메일 주소 입력을 위한 필드 정의
       datetime | - 날짜(년,월,일)과 시간을 함께 표시할 수 있음
       number | - 슬라이드 막대를 사용해 숫자를 입력
       tel | - 전화번호 입력을 위한 필드 정의
       search | - 검색 문자열 입력을 위한 텍스트 필드 정의

  - video
    - `video` 태그는 HTML5 에서는 다른 추가 플러그인 없이 비디오와 오디오의 미디어에 대한 재생이 가능하도록 지원해준다. 동영상 콘텐츠를 포함하기 위해 사용하며 `src`속성이나 `<source>`요소를 이용해 여러개의 동영상 소스를 표시 할 수 있고 브라우저에 가장 적절한 것을 선택해서 사용한다.

      - `video` 사용 예
        ```html
        <video class="news-video" src="/media/stories.mp4" poster="/media/poster.jpg" controls preload="auto" autoplay>
        ```
    
    - Attributes

      속성 | 값 | 설명
      ----- | ----- | -----
      src | URL | - 삽입할 동영상의 주소, 재생할 미디어의 URL을 나타낸다
      height | px(숫자) | - 비디오 높이의 픽셀 값
      width | px(숫자) | - 비디오 넓이의 픽셀 값
      controls |"controls", "", - | - 비디오의 재생, 볼륨 등 제어 조절 장치를 보여주며,  "controls"나 공백이나 태그 안에 값 없이 controls만 적어줘도 적용된다.
      muted | "muted", "", -| - 음소거, 비디오의 포함된 오디오를 음소거 할지 지정(기본값 false)
      poster | URL | - 비디오가 로드되지 않고 있을때 처음에 표시될 이미지의 URL
      loop | "loop", "", - | - 이 속성이 설정 되어 있으면 동영상을 계속 반복한다.
      preload | "none", "metadata", "auto" | - 페이지를 읽을 때 미디어도 같이 읽어들여 재생을 준비한다.<br/>- `none` : 비디오 파일을 로드하지 않음<br/>- `metadata` : metadata만 로드 함<br/>- `auto`: 전체 비디오 파일을 로드함

    - `track` 태그  
      트랙 엘리먼트는 미디어 요소(`audio`,`video`)의 자식 요소이며, 외국어에 대한 자막, 장애인들을 위한 자막, 스크린 리더가 읽는 글을 비디오나, 오디오에 추가를 해줄수 있도록 한다. vtt의 파일 확장자 명을 가진다.
      
      - `track` 사용 예
        ```html
        <video src="media/stories.mp4">
        <track src="media/stories_ko.vtt" kind="captions" srclang="ko" label="korean Caption"">
        <track src="media/stories_en.vtt" kind="captions" srclang="en" label="English Caption"">
        </video>
        ```
      - Attributes

        속성|설명
        -----|-----
        kind|텍스트 트랙의 종류를 정의한다.
        src|텍스트 트랙의 데이터의 주소(.vtt 파일)를 정의한다. 이 속성은 반드시 정의가 되어야한다.
        srclang|텍스트 트랙의 데이터의 언어를 정의한다.
        label|브라우저가 사용 가능한 텍스트 트랙을 나열할 때 사용자가 읽을 수 있는 트랙제목.
        default|기본 트랙을 정의.

## 2. Today I found out
   - 사용자가 어떤 브라우저를 사용하는지 알 수 없는 상황에서, 어떤 브라우저든 지원하기위해 source tag를 여러 개 써서 링크하는것도 video태그를 잘 이용 하는 방법중에 하나인 것 같다.

## 3. Ref
   - [HTML5 video 요소의 사용 예](http://craftymind.com/factory/html5video/CanvasVideo.html)  
   - [track 요소 참고 사이트](http://html5ref.clearboth.org/html5:element:track)