# 6/05(화)

## 1. Today I learned

### 1-1 React

#### JSX
- JSX란?
  ```js
  const element = <h1>Hello, world!</h1>;
  ```
  - 위와 같은 문법을 JSX라 부르며, 자바스크립트의 확장 문법이다. JSX를 React 함께 사용하면, UI가 실제로 어떻게 보일지 서술 할 수 있다. 템플릿 언어처럼 보이지만, 오로지 자바스크립트 기반으로 동작하고 있음.

  - JSX는 React '요소'를 만든다.

- Why JSX?  
  
#### 요소 렌더링
- 

```js
  tick() {
  // 상태를 바꿈으로써 화면이 간접적으로 다시 그려지도록 서술
    this.setState({
      date: new Date()
    });
  }
  //상태로부터 화면이 어떻게 그려야져야 하는지를 render메소드에 서술
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
```