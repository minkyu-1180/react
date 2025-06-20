# 리액트 이론

## Ch05. Props & State

### Props

Props(속성) : 부모 컴포넌트가 자식 컴포넌트에게 전달하는 데이터

- 부모 컴포넌트에서 컴포넌트 사용 시, HTML 속성처럼 전달
- 자식 컴포넌트는 전달받은 props에 접근 가능
  - 직접 수정 불가(props : immutable)
- 하향식 데이터 흐름

```jsx
// Parent
import Child from './Child';
function Parent() {
  const userName = '김민규';
  return (
    <div>
      <Child name={userName} />
    </div>
  );
}

// Child
import Parent from './Parent';
function Child(props) {
  return (
    <div>
      <p>안녕하세요, {props.name}님!</p>
    </div>
  );
}
```

### State

State(상태) : 컴포넌트 내부에서 관리되는 데이터

- 변경 가능한 동적 데이터를 다루기 위해 사용
- 가변적(Mutable)
  - state를 직접 수정하지는 않음
  - state를 업데이트해주는 함수를 사용하여 수정(set변수명)
- state가 업데이트 될 경우, React는 해당 컴포넌트와 그 자식 컴포넌트를 자동으로 리렌더링하여 변경된 UI 화면에 반영
- 비동기적으로 state를 업데이트
- useState Hook을 통해 state 관리 가능

#### State 적용 방법

1. useState 훅을 임포트한다
2. 컴포넌트 내부에 state 변수와 state 업데이트 함수를 정의한다

- const [변수명, set변수명] = useState(초기값);
  - 변수명 : state 변수를 저장할 변수
  - set변수명 : state를 변경하기 위해 호출할 함수
  - 초기값 : 처음 state 변수에 저장될 값

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  function increaseCount() {
    setCount(count + 1);
  }
  function decreaseCount() {
    setCount(count - 1);
  }

  return (
    <div>
      <p>현재 카운트: {count}</p>
      <button onClick={increseCount}>증가</button>
      <button onClick={decreseCount}>감소</button>
    </div>
  );
}
```

#### 여러 타입의 state 변수 사용

1. 배열 상태 관리

- 추가 : set변수명([...변수명, 새로운요소]);
  - 기존 state 변수에 저장된 배열에 새로운 요소를 추가하는 방법
- 삭제 : filter(item => item.id !== id);
  - 기존 state 변수에 저장된 배열에서 특정 id값을 가진 요소를 제거하는 방법
- 수정 : map(item => {값에 따른 return});
  - 기존 state 변수에 저장된 배열에서 특정 id값을 가진 요소의 속성을 수정하는 방법

```jsx
function TodoList() {
  const [todos, setTodos] = useState([
    { id: 1, text: 'React 공부하기', done: false },
    { id: 2, text: '코딩 테스트 준비', done: true },
  ]);
  const [newTodoText, setNewTodoText] = useState('');

  const handleAddTodo = () => {
    if (newTodoText.trim() === '') return;

    const newTodo = {
      id: Date.now(), // 간단한 고유 ID 생성
      text: newTodoText,
      done: false,
    };

    //
    setTodos([...todos, newTodo]);

    setNewTodoText(''); // 입력 필드 초기화
  };
  const handleRemoveTodo = (id) => {
    const nextTodos = todos.filter((todo) => todo.id !== id);
    setTodos(nextTodos);
  };

  const handleUpdateTodo = (id) => {
    const nextTodos = todos.map((todo) => {
      if (todo.id === id) {
        return { ...todo, done: !todo.done };
      } else {
        return todo;
      }
    });
    setTodos(nextTodos);
  };
  return (
    <div>
      <h2>할 일 목록</h2>
      <input
        type="text"
        value={newTodoText}
        onChange={(e) => setNewTodoText(e.target.value)}
      />
      <button onClick={handleAddTodo}>추가</button>
      <ul>
        {todos.map((todo) => (
          <li
            key={todo.id}
            style={{ textDecoration: todo.done ? 'line-through' : 'none' }}
          >
            {todo.text} <button onClick={handleRemoveTodo}>삭제</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
export default TodoList;
```
