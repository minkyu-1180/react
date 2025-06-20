# 리액트 이론

## Ch02. 리액트 설치 방법

### 리액트 설치 방법

1. Node.js와 npm 설치

- Node.js : Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타입
  - 기존 웹 브라우저 안에서만 동작 가능하도록 설계된 JavaScript를 웹 브라우저 밖에서도 실행 가능하게 해주는 런타임 환경 제공
  - 개발 도구(Create React App, Webpack, Babel), 개발 서버(npm start), 패키지 관리(npm)등을 위해 필요함
- npm(Node Package Manager) : Node.js 생태계에서 가장 널리 사용되는 패키지 관리자
  - 패키지 설치(npm install), 패키지 관리(dependencies, devDependencies 등), 스크립트 실행(start, build, test), 패키지 공유, 라이브러리 설치, 프로젝트 의존성 관리 등을 위해 필요
- node -v를 통해 cmd에서 Node.js 설치 버전 확인 가능
- npm -v를 통해 cmd에서 npm 설치 버전 확인 가능

2. Create React App을 통해 프로젝트 생성

- CRA(Create React App) : React 애플리케이션을 빠르고 쉽게 시작할 수 있도록 미리 설정된 개발 환경을 제공하는 도구
- 개발자가 개발 환경 구축의 복잡함을 겪지 않고 애플리케이션 코드 작성에 집중할 수 있도록 돕는 Boilerplate 역할
- 복잡한 설정 없이 바로 개발 가능
- `npm create-react-app [앱 이름]`명령어를 통해 React 앱 설치 가능

3. 구조 파악
   '''
   my-react-app/
   ├── node_modules/ # 프로젝트에 필요한 라이브러리들이 설치되는 폴더
   ├── public/ # 정적 파일 (HTML, 이미지 등)을 두는 폴더
   │ ├── favicon.ico
   │ ├── index.html # 애플리케이션의 기본 HTML 파일
   │ ├── logo192.png
   │ ├── logo512.png
   │ ├── manifest.json
   │ └── robots.txt
   ├── src/ # 소스 코드를 작성하는 폴더 (가장 중요!)
   │ ├── App.css
   │ ├── App.js # 메인 컴포넌트 파일
   │ ├── App.test.js
   │ ├── index.css
   │ ├── index.js # 애플리케이션의 시작점
   │ ├── logo.svg
   │ └── reportWebVitals.js
   ├── .gitignore # Git에서 추적하지 않을 파일/폴더 목록
   ├── package.json # 프로젝트 정보 및 의존성 목록
   ├── README.md # 프로젝트 설명 파일
   └── package-lock.json (또는 yarn.lock) # 설치된 패키지 버전 정보
   '''
4. 개발 서버 실행

- `cd [앱 이름]` 명령어를 통해 리액트 애플리케이션 디렉토리로 이동
- `npm start` : 개발 서버 실행 명령어
