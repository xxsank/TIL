# 6/11(월)

## 1. Today I learned

### 1-1 React

#### Ref와 DOM
- **Ref**는 render 메소드에서 생성된 DOM 노드 혹은 React 엘리먼트 객체에 접근할 수 있는 방법을 제공한다.

- 자식 엘리먼트를 수정하기 위해 새 prop을 가지고 다시 렌더링을 해준다. 하지만 가끔은 전형적인 데이터 흐름 밖에서 자식을 명령형으로 변경해야 할 필요가 있다.

- ref 사용할 시점
  - 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때
  - 명령형 애니메이션을 발동시킬 때
  - 서드파티 DOM 라이브러리를 통합할 때

- DOM API를 써야할 때,

- **Ref 생성하기**
  - Ref는 `React.createRef()`를 통해 생성

    ```js
    class MyComponent extends React.Component {
      constructor(props) {
        super(props);
        this.myRef = React.createRef();
      }
      render() {
        return <div ref={this.myRef} />;
      }
    }
    ```

- **Ref 사용하기**
  - `render()` 메소드에서 반환하는 엘리먼트에 ref가 넘겨지면, ref의 `current` 속성을 통해 해당 노드에 접근할 수 있다.

    ```js
    const node = this.myRef.current;
    ```
    - HTML 엘리먼트에 ref 어트리뷰트가 사용되면, ref의 current 속성은 DOM 엘리먼트 객체를 가리킵니다.

    - 클래스 컴포넌트에 ref 어트리뷰트가 사용되면, ref의 current 속성은 해당 컴포넌트로부터 생성된 인스턴스를 가리킵니다.

    - **함수형 컴포넌트는 인스턴스를 가질 수 없기 때문에 ref 어트리뷰트 역시 사용할 수 없습니다.**