# 5/23(수)

## 1. Today I learned

### 1-1. 게시판 만들기 실습 추가기능 구현

#### 삭제 기능
- html 문서의 `post-content` template에 class 추가
  ```html
  <button class="post-content__delete-btn">삭제</button> 
  ```

- 로그인만 했을때 수정,삭제 버튼이 나오도록 하기
  ```scss
  .post-content{
    &__delete-btn, &__modify-btn{
      display: none;
      .root--authed & {
        display: inline-block;
      }
    }
  }
  // 이미 로그인했을때 root에 addclass가 추기되있는 작업을 했으므로 css만 추가함
  ```

- 게시글 클릭후 나오는 ContentPage에서 삭제 버튼 눌렀을때 해당 글 삭제
  - postContentPage 비동기 함수에 추가
  ```js
  fragment.querySelector('.post-content__delete-btn').addEventListener('click', async e=>{
    await postAPI.delete(`/posts/${postId}`);
    indexPage();
  })
  ```

#### 수정 기능
- html 문서의 `post-content` template에 class 추가
  ```html
  <button class="post-content__modify-btn">수정</button> 
  ```

- 새로운 수정페이지를 위한 template 작성
  ```html
  <!-- 사실 post-form에서 이름만 수정해서 추가했다. -->
  <template id="modify-form">
    <form class="modify-form">
      <h1 class="modify-form__header">수정 하기</h1>
      <input name="title" type="text" class="modify-form__title">
      <textarea name="body" class="modify-form__body"></textarea>
      <button class="modify-form__submit-btn">전송</button>
      <button class="modify-form__back-btn">뒤로 가기</button>
    </form>
  </template>
  ```

- 로그인만 했을때 수정,삭제 버튼이 나오도록 하기
  ```scss
  .post-content{
    &__delete-btn, &__modify-btn{
      display: none;
      .root--authed & {
        display: inline-block;
      }
    }
  }
  ```

- 게시글 클릭후 나오는 ContentPage에서 삭제 버튼 눌렀을때 해당 글 삭제
  - postContentPage 비동기 함수에 추가
  ```js
  fragment.querySelector('.post-content__modify-btn').addEventListener('click', e=>{
    modifyFormPage(postId);
  })
  ```

- 수정된 페이지가 나올수 있도록 함수 생성
  ```js
    // 수정기능 구현
  async function modifyFormPage(postId){
    const res = await postAPI.get(`/posts/${postId}`);
    const fragment = document.importNode(templates.modifyForm, true);
    fragment.querySelector('.modify-form__title').value = res.data.title;
    fragment.querySelector('.modify-form__body').value = res.data.body;

    // 수정페이지에서 뒤로가기버튼 구현 , 뒤로가기를 누르면 수정하려던 원래본문으로 돌아간다
    fragment.querySelector('.modify-form__back-btn').addEventListener('click', e=>{
      e.preventDefault();
      postContentPage(postId);
    })
    
    // 수정페이지에서 수정 submit event 구현
    fragment.querySelector('.modify-form').addEventListener('submit', async e=>{
      e.preventDefault();
      const payload = {
        title: e.target.elements.title.value,
        body: e.target.elements.body.value
      };
      const res = await postAPI.patch(`/posts/${postId}`,payload);
      console.log(res);
      postContentPage(res.data.id);
    })
    render(fragment);
  }
  ```