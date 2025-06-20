# 리액트 이론

## Ch07. 리액트 훅

### UseEffect

UseEffect : 함수형 컴포넌트에서 Side Effects(컴포넌트의 렌더링 결과인 UI 외에 발생하는 모든 작업)를 수행할 수 있게 해주는 React Hooks

- 데이터 가져오기(Fetching Data)
- 구독 설정(Setting Up Subscription)
- 수동 DOM 조작(Manually Changing the DOM)
- 타이머 설정(setTimeout, setInterval 등)
- 로컬 스토리지 사용

#### useEffect의 구조

useEffect(setup, dependencies)

- setup : 부수 효과 로직을 담는 함수
  - 컴포넌트 렌더링 후 실행되는 함수
  - 필수
  - 필요 시, Cleanup 함수 반환 가능
- dependencies : 이펙트가 다시 실행되어야 하는 조건을 담은 배열
  - 해당 배열 내에 담긴 값(변수, state, props 등)이 변경 될 때 마다 setup 함수가 다시 실행됨
  - 빈 배열일 경우, 첫 렌더링 시에만 setup 함수 실행
  - 배열을 생략한 경우, 렌더링 될 때 마다 setup 함수가 실행(무한루프 주의 -> 사용하지 않는게 좋음)
  - 배열 내에 여러 요소들이 있을 경우, 값이 하나라도 변경 될 때마다 setup 함수가 실행

#### Cleanup

Cleanup 함수 : useEffect의 첫 번째 인자로 전달되는 setup함수에서 선택적으로 반환하는 함수

- 컴포넌트 렌더링 이후, useEffect를 통해 SideEffect 수행
- 부수적인 작업을 마친 후, 뒷정리가 필요
- 뒷정리를 하지 않으면..
  - 메모리 누수
  - 예상치 못한 동작
- useEffect가 실행됨으로써 남겨진 흔적을 지워주는 함수

cleanup 함수가 실행되는 시점

1. 의존성 배열이 존재하는 경우

- 다음 useEffect가 실행되기 직전마다(언마운트 될 때 포함) 시행

2. 빈 의존성 배열일 경우

- 컴포넌트가 언마운트 될 때 한 번 시행

3. 의존성 배열이 없는 경우

- 초기 렌더링을 제외하고 렌더링될 때 마다 시행

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('이펙트: 타이머 시작');
    const intervalId = setInterval(() => {
      setCount((prevCount) => prevCount + 1);
    }, 1000);

    // ➡️ cleanup 함수 반환
    return () => {
      console.log('클린업: 타이머 중지');
      clearInterval(intervalId);
    };
  }, []); // 빈 배열: 마운트 시 타이머 시작, 언마운트 시 타이머 중지

  return (
    <div>
      <p>타이머: {count}초</p>
    </div>
  );
}
export default Timer;
```

### useRef

useRef : current 속성을 가진 변경 가능한 객체를 반환

- const refContainer = useRef(initialValue);
  - initialValue : .current 속성 초기값
  - refContainer.current : 해당 객체의 current 속성에 실제 저장되는 값

useRef 사용 목적

1. DOM 엘리먼트에 직접 접근

- 일반적으로 Virtual DOM을 통해 UI 관리
- 때로는 특정 DOM 엘리먼트(ex. input, div, canvas 등)에 직접 접근해서 조작할 필요가 있음
- 특정 DOM 엘리먼트에 대한 참조를 얻을 수 있음

```jsx
import React, { useRef, useEffect } from 'react';

function FocusInput() {
  // input 엘리먼트를 참조할 ref 객체 생성
  const inputElement = useRef(null);

  useEffect(() => {
    // 컴포넌트가 마운트된 후 (초기 렌더링 후) 실행
    // inputElement.current는 <input> DOM 엘리먼트를 가리킵니다.
    if (inputElement.current) {
      inputElement.current.focus(); // input 엘리먼트에 포커스 설정
    }
  }, []); // 빈 의존성 배열: 마운트될 때 한 번만 실행

  return (
    <div>
      {/* input 엘리먼트의 ref 속성에 inputElement ref 객체 연결 */}
      <input type="text" ref={inputElement} />
      <p>페이지 로드 시 자동으로 포커스됩니다.</p>
    </div>
  );
}
export default FocusInput;
```

2. 렌더링 사이에 리렌더링 없이 변경 가능한 값을 유지하기

- 컴포넌트 전체 생명주기 동안 유지되어야 하지만, 값이 변경되어도 컴포넌트 리렌더링 유발 X
- useState로 관리하는 상태 : 값이 변경 될 때 마다 컴포넌트를 리렌더링시킴
- useRef로 관리하는 current : 값이 변경 되어도 리렌더링 X

```jsx
import React, { useState, useEffect, useRef } from 'react';

function StateChangeTracker() {
  const [count, setCount] = useState(0);
  // 이전 count 값을 저장할 ref 객체 생성
  const prevCountRef = useRef(null);

  useEffect(() => {
    // count 값이 변경될 때마다 실행 (초기 렌더링 후에도 실행)
    // 현재 count 값을 prevCountRef.current에 저장
    prevCountRef.current = count;
    console.log(
      `현재 count: ${count}, 이전 count (ref): ${prevCountRef.current}`
    );
  }, [count]); // count 값이 변경될 때마다 이펙트 실행

  const prevCount = prevCountRef.current; // ref에 저장된 이전 값 읽기

  return (
    <div>
      <p>현재 카운트: {count}</p>
      {/* prevCount는 useEffect가 실행된 후 업데이트되므로,
          렌더링 시점에서는 직전 렌더링의 count 값이 됩니다. */}
      <p>이전 카운트 (ref 사용): {prevCount !== null ? prevCount : '없음'}</p>
      <button onClick={() => setCount(count + 1)}>증가</button>
    </div>
  );
}
export default StateChangeTracker;
```

### useContext

useContext : 컴포넌트 트리 내부의 데이터를 props drilling 없이 전역적으로 공유할 수 있게 해주는 React Context API 접근에 사용하는 Hook

- 여러 단계의 컴포넌트를 거쳐 props를 전달하는 것이 번거로울 경우, Context를 사용하여 데이터를 필요로 하는 하위 컴포넌트에서 직접 접근 가능

useContext 사용 방법

1. React.createContext()를 통해 Context 객체 생성

- const Context객체명 = createContext(기본값);

2. 데이터를 제공하는 상위 컴포넌트에서 Context.Provider를 사용하여 Context 값을 제공

- `<Context객체명.Provider value="새로운값"><하위컴포넌트 /></Context객체명.Provider>`

3. 데이터를 제공받아 사용할 하위 컴포넌트에서 useContext(Context객체)를 호출하여 Context 값을 가져옴

- const 변수명 = useContext(객체명)

```jsx
// 1. Context 생성 (어떤 파일이든 가능)
import React, { createContext, useContext } from 'react';

const ThemeContext = createContext('light'); // 기본값 'light'

// 2. Provider 사용 (상위 컴포넌트)
function App() {
  return (
    // ThemeContext.Provider로 감싸고 value prop으로 값 전달
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// 3. useContext 사용 (하위 컴포넌트)
function Toolbar() {
  // useContext Hook을 사용하여 ThemeContext의 현재 값 가져오기
  const theme = useContext(ThemeContext);
  return (
    <div
      style={{
        background: theme === 'dark' ? '#333' : '#EEE',
        color: theme === 'dark' ? '#EEE' : '#333',
      }}
    >
      현재 테마: {theme}
    </div>
  );
}
export default App; // 또는 Toolbar 등 필요한 컴포넌트 내보내기
```
