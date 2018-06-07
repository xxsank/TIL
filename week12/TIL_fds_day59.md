# 6/07(수)

## 1. Today I learned

### 1-1 React

#### 리스트와 키

- 컴포넌트 여러 개를 렌더링 하기
  - 요소 목록을 만든 뒤에는 중괄호 `{}`를 사용하여 `JSX`에 포함 시키는 것이 가능함.

  ```js
  const numbers = [1, 2, 3, 4, 5];
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  ```

  - 전체 `listItems` 배열을 `<ul>` 요소 안에 삽입해서 DOM에 렌더링 해줄 수 있다. 

  ```js
  ReactDOM.render(
    <ul>{listItems}</ul>,
    document.getElementById('root')
  );
  ```

- 기본적인 목록 컴포넌트

  ```js
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <li>{number}</li>
    );
    return (
      <ul>{listItems}</ul>
    );
  }

  const numbers = [1, 2, 3, 4, 5];
  ReactDOM.render(
    <NumberList numbers={numbers} />,
    document.getElementById('root')
  );
  ```

  - 이 코드를 실행하면, 목록의 각 항목에 키를 넣어야 한다는 경고가 표시된다. `키(key)`는 요소 목록를 만들 때 포함해야하는 특수한 문자열 속성이다.
  - 목록 데이터를 렌더링 할 때는 `key`라는 prop을 리액트가 받아야 정상적으로 렌더링을 시켜준다
  - map callback에서 반환하는 요소에는 `key`를 반드시 넣어주어야 하며, index값은 넣어주지 않는게 좋다.

#### 키

- 키를 지정해주면 어떤 아이템이 바뀌었는지, 추가되었는지, 삭제되었는 지를 React에게 알려줄 수 있다. 배열에 들어있는 요소마다 식별자를 키로 넣어주자.

  ```js
  const numbers = [1, 2, 3, 4, 5];
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  ```

  - 키로 쓰기에 가장 적절한 값은 각 항목을 고유하게 식별할 수 있는 문자열이다, 대부분의 경우 데이터의 ID를 키로 사용한다.

  ```js
  const todoItems = todos.map((todo) =>
    <li key={todo.id}>
      {todo.text}
    </li>
  );
  ```

  - 항목 간 순서가 바뀔 수 있는 경우 키에 인덱스를 사용하지 않는게 좋다. 

- **잘못된 키 사용법**

  ```js
  function ListItem(props) {
    const value = props.value;
    return (
      /* 틀렸습니다! 여기서 키를 넣어주는 것은 아무런 효과가 없습니다.*/
      <li key={value.toString()}>
        {value};
      </li>
    );
  }

  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      /* 틀렸습니다! 바로 여기서 키를 넣어주어야 합니다. */
      <ListItem value={number} />
    );
    return (
      <ul>
        {listItems};
      </ul>
    );
  }

  const numbers = [1, 2, 3, 4, 5];
  ReactDOM.render(
    <NumberList numbers={numbers} />,
    document.getElementById('root')
  );
  ```

- map() 에서 반환하는 요소에는 키를 넣어준다










#### 폼
- HTML 폼(form) 요소는 그 자체가 내부 상태를 가지기 때문에, React에서는 다른 DOM 요소들과는 조금 다르게 동작한다. 예를 들어, 순수한 HTML에서 이 폼은 이름을 입력받는다.

  ```js
  <form>
    <label>
      Name:
      <input type="text" name="name" />
    </label>
    <input type="submit" value="Submit" />
  </form>
  ```

  - 위 폼에서 유저가 폼을 전송(submit)하면, 새로운 페이지로 이동하는 기본 HTML 폼 동작을 수행합니다. 만약 React에서 똑같은 동작을 원한다면, 그냥 그렇게 사용하면 됩니다. 그러나 대부분의 경우, 자바스크립트 함수를 만들어서 form 제출을 처리하고 사용자가 form에 입력한 데이터에 접근하도록 만드는 게 좋습니다. 이를 위해 널리 사용되는 방식은 **제어되는 컴포넌트 (Controlled Components)** 를 사용하는 것입니다.

- **제어되는 컴포넌트**
  - HTML에서 `<input>`, `<textarea>`, `<select>` 같은 form 요소는 자기만의 상태를 가지고 사용자의 입력에 따라 업데이트됩니다. 반면에 React에서는, 변경 가능한 상태를 일반적으로 컴포넌트의 state 속성에 위치시키며, 이는 `setState()`로만 업데이트할 수 있습니다.

  - React state를 `진리의 유일한 원천 (single source of truth)`으로 만들어 두 세계를 결합할 수 있습니다. 이렇게 하면 사용자의 입력에 따라 폼에서 발생되는 일을 React 컴포넌트 측에서 제어하게 됩니다. 이런 방식으로, React에 의해 제어되는 input 폼 요소를 **제어되는 컴포넌트** 라고 부릅니다.

  ```js
  class NameForm extends React.Component {
    constructor(props) {
      super(props);
      this.state = {value: ''};

      this.handleChange = this.handleChange.bind(this);
      this.handleSubmit = this.handleSubmit.bind(this);
    }

    handleChange(event) {
      this.setState({value: event.target.value});
    }

    handleSubmit(event) {
      alert('A name was submitted: ' + this.state.value);
      event.preventDefault();
    }

    render() {
      return (
        <form onSubmit={this.handleSubmit}>
          <label>
            Name:
            <input type="text" value={this.state.value} onChange={this.handleChange} />
          </label>
          <input type="submit" value="Submit" />
        </form>
      );
    }
  }
  ```

  - `value` 어트리뷰트가 폼 요소에 설정되었기 때문에, 표시되는 값은 항상 `this.state.value` 가 됩니다. 즉, React state가 진리의 유일한 원천이 됩니다. 키 입력이 일어날 때마다 `handleChange` 가 동작하고 React state가 업데이트되므로, 표시되는 값은 사용자의 입력에 따라 업데이트 됩니다.

- **textarea 태그**
  - html에서의 `<textarea>` 태그

    ```html
    <textarea>
      Hello there, this is some text in a text area
    </textarea>
    ```
    - html에서의 요소는 필드 내부의 텍스트를 자식으로서 지정한다.
  
  - react에서의 `<textarea>` 태그

    ```js
    class EssayForm extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          value: 'Please write an essay about your favorite DOM element.'
        };

        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this);
      }

      handleChange(event) {
        this.setState({value: event.target.value});
      }

      handleSubmit(event) {
        alert('An essay was submitted: ' + this.state.value);
        event.preventDefault();
      }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Essay:
              <textarea value={this.state.value} onChange={this.handleChange} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    ```
    - React에서 `<textarea>` 는 대신 value 어트리뷰트를 사용합니다. 이렇게 하면 `<textarea>` 를 사용하는 폼은 한 줄 짜리 입력 필드와 매우 유사하게 작성할 수 있습니다.
    
    - `this.state.value` 를 생성자 함수에서 초기화하기 때문에, 텍스트를 가진 채로 textarea를 표시해줄 수 있습니다.






#### State 끌어올리기
- 