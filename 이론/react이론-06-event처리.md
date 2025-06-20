# 리액트 이론

## Ch06. 이벤트 처리

### Event

React의 Event 처리 방법 : DOM에서 이벤트를 처리하는 것과 비슷

- 이벤트 이름 : camelCase로 작성(onclick => onClick)
- 이벤트 핸들러 전달 : 문자열이 아닌 함수 자체를 중괄호`{}`에 담아서 전달(onClick={handleClick})

### React에서 사용하는 이벤트 종류

1. onClick : 클릭 시 특정 함수를 실행하는 함수

- onClick={클릭시호출되는함수명}
- 함수명 옆에 괄호`()` 작성 시, 컴포넌트가 렌더링 될 때 함수가 즉시 실행됨(주의!!!)

```jsx
import React from 'react';

function MyButton() {
  const handleClick = () => {
    alert('버튼이 클릭되었습니다!');
  };

  return <button onClick={handleClick}>클릭하세요</button>;
}
export default MyButton;
```

2. onChange : input, textarea, select 등의 form 엘리먼트에서 값이 변경될 때 발생하는 이벤트

- onChange={변경시호출되는함수명}
- 인자로 event를 전달하여, 현재 발생한 event가 바라보고있는 target의 value에 접근하여 변경하면 됨(event.target.value)
- state변수를 변경시키는 함수와 함께 자주 사용

```jsx
import React, { useState } from 'react';

function MyInput() {
  const [text, setText] = useState(''); // 입력 필드의 현재 값을 관리하는 state

  const handleChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <input type="text" value={text} onChange={handleChange} />
      <p>입력된 값: {text}</p>
    </div>
  );
}
export default MyInput;
```

3. onSubmit : form 엘리먼트에서 제출 될 때 발생하는 이벤트

- submit 타입의 버튼을 클릭할 때, onSubmit과 연결된 함수가 호출 될 수 있도록 form태그의 onSubmit과 연결
- event.preventDefault() 함수를 호출하여 페이지가 새로고침되는 기본 동작을 막을 수 있음

```jsx
import React, { useState } from 'react';

function MyForm() {
  const [inputValue, setInputValue] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();

    alert(`제출된 값: ${inputValue}`);
    setInputValue('');
  };

  const handleInputChange = (event) => {
    setInputValue(event.target.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={inputValue} onChange={handleInputChange} />
      <button type="submit">제출</button>
    </form>
  );
}
export default MyForm;
```
