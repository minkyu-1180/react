# 리액트 이론

## Ch04. JSX

### JSX

JSX(JavaScript XML) : JavaScript의 확장 문법

- React 엘리먼트 생성을 위해 사용
- 겉보기에는 HTML과 매우 유사하지만, 실제로는 JavaScript 코드 안에서 UI 구조를 표현하기 위해 사용

#### JSX 사용 이유

JSX 사용 이유는 무엇일까?

- React는 UI 구성 로직(JavaScript), UI 구조(HTML)를 분리하는 대신, 서로 관련된 로직과 마크업을 컴포넌트 안에 함께 작성하는 방식을 선호
- JSX는 이러한 방식에 맞춰서 JS 코드 안에서 직관적으로 UI 구조를 작성할 수 있도록 돕는 문법이다

JSX를 사용함으로 인해

1. 가독성 향상 : UI 구조를 HTML 처럼 작성 가능
2. 개발 생산성 : JavaScript 로직과 UI 구조를 한 곳에서 관리
3. 런타임 성능 : Babel에 의해 JSX가 일반 JavaScript 객체로 변환 -> 변환된 객체를 사용하여 Virtual DOM에 효율적으로 업데이트

#### JSX 사용 규칙

JSX는 HTML과 비슷하지만, 여러 차이점이 존재합니다 ~.~

1. 하나의 루트 엘리먼트

- JSX 코드는 반드시 하나의 Root Element로 감싸야 한다
- 여러 엘리먼트를 병렬적으로 반환 불가
- `<React.Fragment></React.Fragment>` 또는 `<></>`로 최상단을 감싸서 해결
  - Fragment : 불필요한 div 생성 방지를 위해 사용하는 속성

2. JavaScript 표현식 사용

- JSX 내부에서 JavaScript 변수 또는 함수 호출 결과를 사용하기 위해 중괄호`{}` 안에 작성

3. 속성명

- 기존 HTML의 class 대신, className이라는 걸 사용
- 기존 HTML의 for 대신, htmlFor이라는 걸 사용
- 문자열 속성은 큰따옴표`""`로 감싸서 사용
- 속성 이름은 일반적으로 camelCase 규칙을 따름
- JavaScript 표현식을 사용할 경우, 속성은 중괄호`{}`로 감쌈

4. Self-closing 태그

- 내용이 없는 태그(ex. img, input, br)는 반드시 닫는 태그를 명시하거나, `/`를 사용한 self-closing 태그로 생성
