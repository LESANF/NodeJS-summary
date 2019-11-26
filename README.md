- [1. Node.js란?](#NodeJS란?)
- [2. 개발환경 세팅](#NodeJS를-세팅하는-법)
- [3. 빠르게 서버 만들기](#express-서버-만들기)
- [4. 라우터](#라우터-Router)
- [5. 미들웨어](#미들웨어-Middleware)
- [6. 템플릿 엔진](#템플릿-엔진-pug)
- [7. res.locals](#템플릿에서-접근이-가능한-속성-res.locals)

# NodeJS란?

비동기 이벤트 주도 JavaScript 런타임으로써 Node.js 는 확장성 있는 네트워크 애플리케이션을 만들 수 있도록 설계, 각 연결에서 콜백이 실행되는데 실행할 작업이 없다면 Node.js는 대기함.

### NodeJS의 특징

- 비동기 I/O처리 / 이벤트 위주
- 빠른 속도
- 단일 쓰레드 / 뛰어난 확장성
- 노 버퍼링
- 라이센스

### NodeJS의 사용처

- 입출력이 잦은 애플리케이션
- 데이터 스트리밍 애플리케이션
- 데이터를 실시간으로 다루는 애플리케이션
- JSON API 기반 애플리케이션
- SPA
  > 이 경우 뛰어난 효율성을 자랑함.

### NodeJS를 쓰지 말아야 할 때

- CPU 사용률이 높은 애플리케이션

---

# Node.js 개발환경 만들기

### 개발환경

1. Git 설치 및 세팅
   - > git config --global user.name "**your name**"
   - > git config --global user.email "**your email**"
     >
     > > **공용컴퓨터에선 --global로 설정 X**
     > > 취향에 따라 WSL을 설치
2. Windows 10 개발자모드 활성화
   - > 설정 > 업데이트&보안 > 개발자 > 개발자모드
     >
     > > ![devenable2](https://user-images.githubusercontent.com/46839654/69611428-13566780-1071-11ea-9286-641ffed52c42.PNG)
   - > Windows 기능 > **리눅스 하위 시스템** 활성화
     >
     > > ![devenable](https://user-images.githubusercontent.com/46839654/69611424-12253a80-1071-11ea-88dd-88d3141f2cec.PNG)
3. NodeJS 설치
   > 자동으로 **npm**이 설치됨.
4. VSC 설치 (텍스트 에디터)
   > 확장프로그램 **Prettier 필수**

---

# 프로젝트 시작하기

### NPM 명령어

1. 콘솔에서 해당 경로 진입 후 **npm init** 입력
2. 정보 입력 후 마무리
3. 필요한 패키지 설치
   > npm install "**패키지 명**" [ -D or -g ]
   - > -D : devDependencies에 설치됨
     >
     > > 생략한 경우 dependencies에 설치됨
   - > -g : 전역으로 설치됨 (다른 프로젝트에도 적용)
   - > "**npm i**" 로 단축할 수 있다.
4. 패키지 삭제
   > npm uninstall "**해당 패키지 명**"
5. 스크립트

- 예약어 npm start
  - > "start" : "node src/server.js" 설정 시
    >
    > > npm start 명령어로 시작
- 그외 명령어
  - > "dev:server" : "node src/server.js" 설정 시
    >
    > > npm run dev:server 명령어로 시작

6. 자주 사용하는 패키지
   - > Babel - @babel/core, @babel/node, @babel/preset-env
     - > Babel 설정
       >
       > > ![babel](https://user-images.githubusercontent.com/46839654/69611403-0a659600-1071-11ea-9fb2-fc748e2516e5.PNG) ![babel_script](https://user-images.githubusercontent.com/46839654/69611417-105b7700-1071-11ea-872a-3f03ce1f0b12.PNG)
   - > express (서버)
   - > nodemon (서버 자동 재시작)
   - > helmet (보안)
   - > cookie-parser (쿠키 이용)
   - > body-parser (업데이트로 기본 내장될 수 있음)
   - > morgan (로깅 미들웨어)
   - > pug (템플릿 엔진)
   - > multer (파일 저장)

---

# express 서버 만들기

![express](https://user-images.githubusercontent.com/46839654/69611438-18b3b200-1071-11ea-8321-bb4828b2d84e.PNG)

![example](https://user-images.githubusercontent.com/46839654/69611434-16e9ee80-1071-11ea-9ebf-e56f0efcafe0.PNG)

> 실제 사용할 때는 express.listen(**port**, **callback**)을 적어야 한다.
>
> > 위의 코드는 @Babel/preset-env가 적용된 상태임. 적용하지 않으면 구형 자바스크립트를 사용해야함.

---

# 라우터 Router

### app.js

![router-app](https://user-images.githubusercontent.com/46839654/69612394-ee62f400-1072-11ea-94f5-121b8f539d73.png)

### router.js

![router-router](https://user-images.githubusercontent.com/46839654/69612395-eefb8a80-1072-11ea-9db3-90e992bb37b1.png)

### results

![router-show](https://user-images.githubusercontent.com/46839654/69612397-eefb8a80-1072-11ea-85fa-cc1409ea632c.png)
![router-show1](https://user-images.githubusercontent.com/46839654/69612398-ef942100-1072-11ea-9740-5fbe0aa770de.png)

> user로 라우터를 연결했다면 userRouter의 /user로 접근하기 위해선 **"/"** 으로 접근해야 한다.

---

# 미들웨어 Middleware

### middleware.js

![middleware-js](https://user-images.githubusercontent.com/46839654/69613479-f885f200-1074-11ea-86e2-001749fe66aa.png)

### router.js

![middleware-route](https://user-images.githubusercontent.com/46839654/69613482-f885f200-1074-11ea-96bb-dd0fb189e4db.png)

### app.js

![middleware-app](https://user-images.githubusercontent.com/46839654/69612924-01c28f00-1074-11ea-95b7-5743189ecdac.png)

### results

![middleware-show](https://user-images.githubusercontent.com/46839654/69613484-f91e8880-1074-11ea-939f-dfe3fdacc0f4.png)

> 라우터 위에 작성하면 경로가 바뀔 때마다 실행된다.
>
> > 어떤 Function이든 미들웨어가 될 수 있다.

---

# 템플릿 엔진 pug

### pug 설치

> npm i pug

### app 설정

![pug-app](https://user-images.githubusercontent.com/46839654/69617587-c1ffa580-107b-11ea-99a4-41b668ef6916.png)

> pug의 default 폴더명은 "**views**"이다. 바꿀 수 있음.
>
> > \_\_dirname은 현재 디렉터리를 표시하고, path.join은 매개변수를 잇는다(join).

### pug 템플릿

- layouts/main

![main-pug](https://user-images.githubusercontent.com/46839654/69617586-c1ffa580-107b-11ea-87d1-ec054e949b84.png)

> pug은 레이아웃 기능을 지원함. (mixins, include, extends)

- partials/header

![header-pug](https://user-images.githubusercontent.com/46839654/69617581-c1670f00-107b-11ea-8cb4-3d8d2116df0d.png)

> 중복적인 부분을 한번만 작성하여 재사용이 가능함.

- home

![home-pug](https://user-images.githubusercontent.com/46839654/69617584-c1670f00-107b-11ea-819a-9c052420e252.png)

> 그 결과, 레이아웃을 불러오고 block content 안에만 채우면 됨.

- 실행 결과

![result-pug](https://user-images.githubusercontent.com/46839654/69617589-c1ffa580-107b-11ea-964b-05183b0d6e95.png)

---

# 템플릿에서 접근이 가능한 속성 res.locals
### middleware.js
![middleware-locals](https://user-images.githubusercontent.com/46839654/69619255-a8ac2880-107e-11ea-8d79-edf4d58edeab.png)

### main.pug
![main-locals](https://user-images.githubusercontent.com/46839654/69619254-a8139200-107e-11ea-94ff-b5f0129e43db.png)

### app.js
![home-locals](https://user-images.githubusercontent.com/46839654/69619253-a8139200-107e-11ea-80d4-d7c18ca7cce6.png)

### results
![result-locals](https://user-images.githubusercontent.com/46839654/69619451-edd05a80-107e-11ea-8135-4ad038b8cd11.png)
> res.render()의 두번째 인자는 특정 템플릿에만 데이터를 넘기지만, **res.locals**는 전역적으로 데이터를 넘김.
