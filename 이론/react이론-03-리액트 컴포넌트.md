# 리액트 이론

## Ch03. 리액트 컴포넌트

### React Component

컴포넌트(Component) : 리액트 애플리케이션에서 레고 블록 처럼 여러 개의 독립적이고 재사용 가능한 UI 단위

- 자체적인 로직(기능)과 모양(UI)를 가짐

#### 컴포넌트의 장점

1. 재사용성

- 한 번 만든 컴포넌트는 애플리케이션의 여러 곳에서 반복적으로 사용 가능

2. 모듈성

- UI를 작은 단위로 나누어 관리
- 깔끔한 코드 작성 가능
- 쉬운 이해

3. 유지보수

- 특정 기능 또는 UI 수정 필요 시, 해당 컴포넌트만 수정하면 됨

#### 컴포넌트 작성 방법

1. 클래스형 컴포넌트(Class Component) : JavaScript의 ES6 클래스 문법을 사용하여 작성하는 컴포넌트

- React.Component 클래스를 상속받아 만들어지는 컴포넌트
  - render() 메서드를 통해 JSX를 반환하여 UI 정의
  - this.props를 통해 부모 컴포넌트로부터 전달받은 데이터에 접근
- 이전 버전의 React에서 주로 사용
- 함수형 컴포넌트 등장 전, 상태 관리, 생명주기 메서드 사용에 필수적으로 사용

```jsx
import React, { Component } from 'react';
class ClassComponent extends Component {
  render() {
    return (
      <div>
        <h1>안녕하세요. {this.props.name}님!</h1>
        <p>이것은 클래스형 컴포넌트 입니다.</p>
      </div>
    );
  }
}
```

2. 함수형 컴포넌트(Functional Component) : 자바스크림트 함수 형태로 작성된 컴포넌트

- 인자로 부모 컴포넌트에서 전달받은 데이터에 접근 가능
- return을 통해 JSX문법으로 작성된 React 엘리먼트를 반환
  - 해당 엘리먼트는 브라우저 렌더링 UI 정의
- export default를 통해 선언한 함수형 컴포넌트를 다른 파일(컴포넌트, 페이지 등)에서 불러와 사용 가능

- 최근 리액트 개발에서 주로 사용

```jsx
// FunctionalComponent
import React from 'react';
function FunctionalComponent(props) {
  return (
    <div>
      <h1>안녕하세요. {props.name}님!</h1>
      <p>이것은 함수형 컴포넌트 입니다.</p>
    </div>
  );
}

export default FunctionalComponent;

// App.jsx
import React from 'react';
import FunctionalComponent from './FunctionalComponent';

function App() {
  return (
    <div>
      <FunctionalComponent name="김민규" />
    </div>
  );
}
```
