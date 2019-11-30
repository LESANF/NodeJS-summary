- [1. Node.js란?](#NodeJS)
- [2. 개발환경 세팅](#프로젝트-시작하기)
- [3. 빠르게 서버 만들기](#express-서버-만들기)
- [4. 라우터](#라우터-Router)
- [5. 미들웨어](#미들웨어-Middleware)
- [6. 템플릿 엔진](#템플릿-엔진-pug)
- [7. res.locals](#템플릿에서-접근이-가능한-속성-locals)
- [8. express.static](#express-static)
- [9. MongoDB 기본 설정](#MongoDB)
- [9-1. MongoDB 데이터 삽입](#MongoDB-모델-만들고-데이터-삽입하기)
- [9-2. Passport-local-mongoose로 회원가입 만들기](#PassportLocalMongoose를-통한-회원가입)
- [10. 민감한 정보, dotenv로 가리자](#dotenv)
- [11. Gulp 시작하기](#Gulp를-시작하는-법)
- [11-1 Gulp_pug](#Gulp-pug)
- [11-2 Gulp SASS](#Gulp-SASS)
- [11-3 Gulp Babel](#Gulp-Babel)

# NodeJS

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
     > > `공용컴퓨터에선 --global로 설정 X`
     > > 취향에 따라 WSL을 설치
2. Windows 10 개발자모드 활성화
   - > 설정 > 업데이트&보안 > 개발자 > 개발자모드
     >
     > > ![devenable2](https://user-images.githubusercontent.com/46839654/69611428-13566780-1071-11ea-9286-641ffed52c42.PNG)
   - > Windows 기능 > **리눅스 하위 시스템** 활성화
     >
     > > ![devenable](https://user-images.githubusercontent.com/46839654/69611424-12253a80-1071-11ea-88dd-88d3141f2cec.PNG)
3. NodeJS 설치
   > 자동으로 `npm`이 설치됨.
4. VSC 설치 (텍스트 에디터)
   > 확장프로그램 `Prettier 필수`

---

# 프로젝트 시작하기

### NPM 명령어

1. 콘솔에서 해당 경로 진입 후 `npm init` 입력
2. 정보 입력 후 마무리
3. 필요한 패키지 설치
   > npm install "`패키지 명`" [ -D or -g ]
   - > -D : devDependencies에 설치됨
     >
     > > 생략한 경우 dependencies에 설치됨
   - > -g : 전역으로 설치됨 (다른 프로젝트에도 적용)
   - > "`npm i`" 로 단축할 수 있다.
4. 패키지 삭제
   > npm uninstall "`해당 패키지 명`"
5. 스크립트

- 예약어 npm start
  - > "start" : "node src/server.js" 설정 시
    >
    > > `npm start` 명령어로 시작
- 그외 명령어
  - > "dev:server" : "node src/server.js" 설정 시
    >
    > > `npm run dev:server` 명령어로 시작

6. 자주 사용하는 패키지
   - > Babel - `@babel/core`, `@babel/node`, `@babel/preset-env`
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

> 실제 사용할 때는 express().listen(**port**, **callback**)을 적어야 한다.
>
> `res.send(expression)`는 문자열을 띄어주고, `res.render("템플릿", {data})`는 템플릿을 보여주고, `res.json(data)`는 json 형태로 data를 반환한다.
>
> > 위의 코드는 @Babel/preset-env가 적용된 상태임. 적용하지 않으면 구형 자바스크립트를 사용해야함.

---

# 라우터 Router

### app.js

![router-app](https://user-images.githubusercontent.com/46839654/69612394-ee62f400-1072-11ea-94f5-121b8f539d73.png)

### router.js

![router-router](https://user-images.githubusercontent.com/46839654/69612395-eefb8a80-1072-11ea-9db3-90e992bb37b1.png)

> `/:id`는 파라미터 변수로, 예를들면 영화 id가 203인 그 영화을 보여줄 때 활용한다.
>
> `파라미터 변수의 값`은 해당 라우터의 콜백 함수에서 `req.params`로 받을 수 있다.
>
> `const { id } = req.params;`

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
> > `어떤 Function이든 미들웨어가 될 수 있다.`

---

# 템플릿 엔진 pug

### pug 설치

> npm i pug
>
> > [공식문서](https://pugjs.org/api/getting-started.html)

### app 설정

![pug-app](https://user-images.githubusercontent.com/46839654/69617587-c1ffa580-107b-11ea-99a4-41b668ef6916.png)

> pug의 default 폴더명은 "`views`"이다. 바꿀 수 있음.
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

# 템플릿에서 접근이 가능한 속성 locals

### middleware.js

![middleware-locals](https://user-images.githubusercontent.com/46839654/69619255-a8ac2880-107e-11ea-8d79-edf4d58edeab.png)

### main.pug

![main-locals](https://user-images.githubusercontent.com/46839654/69619254-a8139200-107e-11ea-94ff-b5f0129e43db.png)

### app.js

![home-locals](https://user-images.githubusercontent.com/46839654/69619253-a8139200-107e-11ea-80d4-d7c18ca7cce6.png)

### results

![result-locals](https://user-images.githubusercontent.com/46839654/69619451-edd05a80-107e-11ea-8135-4ad038b8cd11.png)

> res.render()의 인자는 (`템플릿 파일명`, `넘길 데이터`) 로 이루어 진다.
>
> 특정 템플릿에만 데이터를 넘기지만, `res.locals`는 전역적으로 데이터를 넘김.

---

# express static

- Express 정적 파일 제공
  > ![static](https://user-images.githubusercontent.com/46839654/69710884-803a3200-1143-11ea-82b1-399dea00bad1.png)
  >
  > > app.use()의 첫번째 인자, 경로를 생략하면 모든 경로에 static이 적용된다.
- 사용 예제
  > ![static](https://user-images.githubusercontent.com/46839654/69718430-b088cd00-1151-11ea-9450-2931572dc980.png)
  >
  > ![pug static](https://user-images.githubusercontent.com/46839654/69711162-ecb53100-1143-11ea-8bd0-48c86a6bc13a.png)
  >
  > ![pugjsstatic](https://user-images.githubusercontent.com/46839654/69711163-ed4dc780-1143-11ea-8f3d-6286f545aac6.png)
  >
  > > static 폴더가 기본값으로 지정되었기 때문에 파일을 지정할 때 이런 형식으로 사용한다.
- 더 많은 정보
  > [Express에서 정적 파일 제공](https://expressjs.com/ko/starter/static-files.html)

---

# MongoDB

NoSQL 데이터베이스 언어임. 더 적은 규칙과 더 적은 절차로 작업이 가능함. 많은 사람들이
MongoDB를 사용하고 있음. 사용하기 엄청 쉽고 직관적임.

- MongoDB 설치 및 MongoAtlas 이용

  > [MongoDB](https://www.mongodb.com/), [MongoAtlas](https://www.mongodb.com/cloud/atlas)
  >
  > > 설치나 설정법은 간단하니 생략

- mongoose 설치
  > npm i mongoose
  >
  > > [공식문서](https://mongoosejs.com/docs/guide.html)
  >
  > > NodeJS를 위한 Object modeling.
- app.js 설정
  > ![db1](https://user-images.githubusercontent.com/46839654/69712888-e7a5b100-1146-11ea-82b3-e479adcd18e3.png)
  >
  > > 서버 실행 전에 db를 connect 해줘야 함. 지금은 테스트용이라 index.js에 포함 시켰다.
- db.js 설정
  > ![db1](https://user-images.githubusercontent.com/46839654/69712779-bf1db700-1146-11ea-8a2b-146a903eca73.png)
  >
  > > Atlas로 진행하는 경우 cluster를 생성하면 도움말이 있다. 설정 값들은 문서를 보고 필요한 것을 사용하자.
- 실행 결과
  > ![connect](https://user-images.githubusercontent.com/46839654/69713074-3ce1c280-1147-11ea-9286-c6b999f48116.png)
  >
  > > 위처럼 handleOpen()이 실행되면 성공적으로 db에 연결이 되었다.

---

# MongoDB 모델 만들고 데이터 삽입하기

### Model

- 모델 생성
  > ![model](https://user-images.githubusercontent.com/46839654/69716271-0dce4f80-114d-11ea-9c34-6fbaa1e6eb3b.png)
  >
  > > 모델을 하나 간단하게 만들었다.
- 모델 불러오기
  > ![modeldb](https://user-images.githubusercontent.com/46839654/69716463-61d93400-114d-11ea-825a-9b83ce4adcf2.png)
  >
  > > 그리고 모델을 불러온다. 따로 모듈들을 모아둔 파일을 하나 만들어도 된다.

### body-parser

form 입력 데이터를 백엔드에서 받으려면 `body-parser` 패키지가 필요하다. 설치를 해보자.

> npm i body-parser
>
> > ![bodyParser](https://user-images.githubusercontent.com/46839654/69716933-7407a200-114e-11ea-94f5-3b25ea8fa719.png)
>
> `app.use(bodyParser...)`는 pug 설정 밑에 적도록 하자.

### req

req, res, next 중 `req`는 `request`의 약어인데, console.log(req)를 하면 전체적인 요청들을 확인할 수 있다. 그 중에서 form 데이터를 받기 위해 req.body를 활용할 것이다.

- form 생성
  > ![UserCreatedForm](https://user-images.githubusercontent.com/46839654/69716219-f98a5280-114c-11ea-8293-2b1280a7ea85.png) > ![form](https://user-images.githubusercontent.com/46839654/69717387-525aea80-114f-11ea-953f-1822d70ec50c.png)
  >
  > > 우선 form을 하나 만들었다.
- 라우터 설정
  > ![reqBody](https://user-images.githubusercontent.com/46839654/69716610-b4b2eb80-114d-11ea-8884-f70aa8206ff8.png)
- 콘솔 결과

  > ![result](https://user-images.githubusercontent.com/46839654/69717603-b2ea2780-114f-11ea-91a0-fd2914c1c85e.png) > ![reqBody](https://user-images.githubusercontent.com/46839654/69717175-e7111880-114e-11ea-8610-d7ae5d37354e.png)

  > `req.body`를 콘솔 찍어보면 form의 데이터가 넘어온다.

### 데이터 삽입

이제 DB에 데이터를 넣어보자.

- 라우터 설정
  > ![UserCreatedcode](https://user-images.githubusercontent.com/46839654/69717739-f6449600-114f-11ea-9e06-d9845dc24f02.png)
  >
  > > 예를들어 video를 하나 업로드 했는데, 업로드에 성공하자 마자 그 video의 detail로 이동하게 만들고 싶다면
  >
  > > `const video = db.create({});` 👉 `res.redirect(video.id);`
  >
  > > 이런 흐름으로 코드를 작성하면 된다. 중간에 에러를 잡아내야 한다면 `try-catch`를 사용한다.
  >
  > > `const { email, password } = req.body;` 👉 const { **템플릿의 input에 설정해둔 name** } = req.body
- 결과
  > ![UserCreatedconsole](https://user-images.githubusercontent.com/46839654/69717740-f6449600-114f-11ea-8ac0-6d68c2b566a7.png)
  >
  > > 정상적으로 DB에 등록이 된 것을 확인할 수 있다.
  >
  > > MongoDB는 자동으로 `_id(Object Id)`가 생기는데, 이를 통해 데이터 관리를 체계적으로 할 수 있다.
  >
  > > 예를들면, `db.users.findOne({id: object._id})`

---

# PassportLocalMongoose를 통한 회원가입

Passport를 통해서 local 로그인을 구현할 수 있다.

### 설치

> npm i `passport` `passport-local`
>
> npm i `express-session` `connect-mongo` `cookie-parser`
>
> > express-session : 세션, connect-mongo : 로그인 유지, cookie-parser : 쿠키 분해
>
> npm i `passport-local-mongoose`
>
> > [공식 문서](https://github.com/saintedlama/passport-local-mongoose)

### 설정

> 코드가 지저분하여 모듈로 나누었다.

- UserSchema.js (Model)
  > ![dawdawdawd](https://user-images.githubusercontent.com/46839654/69728116-36634300-1167-11ea-8b80-fd337b4efa86.png)
  >
  > > `passport-local-mongoose`를 import하고 UserSchema에 플러그인을 사용한다.
  >
  > > UserSchema에만 passport-local-mongoose 플러그인을 사용하면 된다.
- passport.js
  > ![adwadaw](https://user-images.githubusercontent.com/46839654/69728902-acb47500-1168-11ea-9f1e-c3b190397c95.png)
  >
  > `serializeUser`는 로그인 성공 시 실행되는 done(null, user)에서 user 객체를 전달받아 `req.session.passport.user`에 user를 집어넣고
  >
  > `deserializeUser`는 실제 서버로 들어오는 요청마다 세션 정보(serialize에 의해 저장된)를 DB의 데이터와 비교하고 해당하는 유저 정보가 존재하면 `req.user`에 저장한다.
  >
  > 만약 passport-local-mongoose를 `사용하지 않는다면` 아래처럼 작성해야 한다.
  >
  > > ![passportOriginal](https://user-images.githubusercontent.com/46839654/69728704-4deefb80-1168-11ea-9356-22f2121fd255.png)
- index.js
  > ![adwadaw](https://user-images.githubusercontent.com/46839654/69731784-d3c17580-116d-11ea-9909-c782587466db.png)
  >
  > > **passport.initialize()**, **passport.session()** 👉 session을 처리하는 이 두가지를 꼭 잊지말고 넣어줘야 한다. (공식문서 참조)
  >
  > > **mongoose**, **connect-mongo** : 서버가 재시작 되면 세션 정보가 사라지기 때문에 DB에 세션을 저장한다.
  >
  > > `18~ 30줄`은 passport-local을 사용하기 위한 필수 설정임.
- globalController.js
  > ![123132](https://user-images.githubusercontent.com/46839654/69732122-63ffba80-116e-11ea-9460-f5b748749a7b.png)
  >
  > > passport-local-mongoose에 의해 제공되는 `db.register({userObject}, password)` 는 비밀번호를 암호화해서 숨긴다.
  >
  > > (실제로 스키마에도 비밀번호를 만들지 않았다)
- globalRouter.js
  > ![globalRouter](https://user-images.githubusercontent.com/46839654/69732025-429ece80-116e-11ea-8ccb-d10520f45687.png)
  >
  > > passport-local-mongoose에 의해 `req.logout()`이 제공된다.
- home.pug
  > ![home](https://user-images.githubusercontent.com/46839654/69732911-d58c3880-116f-11ea-8b63-2a29a3d7c579.png)
  >
  > > 로그인 정보, 로그인, 회원가입, 로그아웃을 간단히 만들었다.
- 실행 결과
  > 최초 접속 시 화면
  >
  > ![a](https://user-images.githubusercontent.com/46839654/69733282-74b13000-1170-11ea-9693-eea150c3cbe5.png)
  >
  > 회원가입
  >
  > ![h](https://user-images.githubusercontent.com/46839654/69733143-3287ee80-1170-11ea-8d93-c528584f49fd.png)
  >
  > > 작동
  >
  > 로그인
  >
  > ![b](https://user-images.githubusercontent.com/46839654/69733310-7ed32e80-1170-11ea-8e89-ecf6a0821c75.png)
  >
  > > res.locals에 의해 `req.user 객체`가 보여진다.

---

# dotenv

> github 등에 코드를 업로드 하게되면 자신의 API key, DB주소 및 계정 등 보여지지 말아야 할 것들이 올라가는 경우가 있다.
>
> 이런 상황을 위해 만들어진 패키지로, 사용법은 매우 간단하다.

> npm install `dotenv`

### 사용법

- 프로젝트 폴더에 **.env** 파일 생성
  > ![dotenv2](https://user-images.githubusercontent.com/46839654/69740486-d4add380-117c-11ea-9688-f72afce4051f.png)
  >
  > db.js
  >
  > ![dotenv](https://user-images.githubusercontent.com/46839654/69740449-c1026d00-117c-11ea-93da-50869b42c959.png)
  >
  > > `dotenv`를 import 한 후, `dotenv.config();` 하고 난 뒤 `process.env.name`으로 사용한다.
  >
  > ![dotenv1](https://user-images.githubusercontent.com/46839654/69740451-c19b0380-117c-11ea-8ac7-383e2df77abe.png)
  >
  > > 중요한 정보는 가려지고 작동은 잘 된다. **꼭 .env를 .gitignore에 등록해야 한다.**

---

# Gulp를 시작하는 법

gulp는 Fractal Innovations과 깃허브 오픈 소스 커뮤니티의 오픈 소스 자바스크립트 툴킷으로, 프론트엔드 웹 개발의 스트리밍 빌드 시스템로 사용된다.

### 모듈번들러

![adwadawdaw](https://user-images.githubusercontent.com/46839654/69810217-be605000-122e-11ea-92a3-98c3700bcc89.png)

> 모듈로 이루어진 scss와 front-end js파일을 각각 하나의 파일로 묶어주면서 구형 브라우저에 지원되게 코드를 트랜스파일 해준다.

### 설치

> npm i `gulp -D`

### 폴더 구조

> ![dawdadwawjsdf](https://user-images.githubusercontent.com/46839654/69811675-f0bf7c80-1231-11ea-888e-9c2d985dd1ef.png)
>
> > `gulpfile.js`은 일단 빈 상태로 생성해둔다.

### package.json

> ![dawdawdcc](https://user-images.githubusercontent.com/46839654/69811920-7e02d100-1232-11ea-92b3-57b71472dece.png)
>
> `npm run dev`를 입력하면
>
> ![dawdghjgh](https://user-images.githubusercontent.com/46839654/69811970-9f63bd00-1232-11ea-8125-7f96f900ee67.png)
>
> 이렇게 실행은 되진 않지만, Using gulpfile을 사용한다고 적혀있다.
>
> `gulpfile.js`에 내용을 채워넣고 다시 `npm run dev`를 입력하면
>
> ![213daawdwadawds](https://user-images.githubusercontent.com/46839654/69812458-83ace680-1233-11ea-89d7-0b63805414ac.png)
>
> > ![adabnhgnf](https://user-images.githubusercontent.com/46839654/69812283-25800380-1233-11ea-86f6-e50b824f8003.png)
>
> 문법 에러가 생기는 것을 볼 수 있다. babel을 사용하지 않아 생기는 에러다.
>
> ![adasdasad](https://user-images.githubusercontent.com/46839654/69812545-accd7700-1233-11ea-8431-c28dde2bc165.png)
>
> 구형 문법으로 작성하면 다시 작동한다. 위에 보면 `Task never defined: dev`라고 빨간 글자가 있는데
>
> 요 에러는 task가 존재하지 않아 나타나는 에러다.
>
> 그런데 우리는 최신 문법을 사용하고 싶지 않은가.

### Babel을 이용한 Gulp

> 필요한 패키지를 설치해보자.
>
> > npm i @babel/core @babel/register @babel/preset-env -D
>
> 그런 다음, .babelrc 파일을 생성하자.
>
> > ![dawdawdawdassas](https://user-images.githubusercontent.com/46839654/69813189-07b39e00-1235-11ea-9238-987e10cf3364.png)
>
> 그리고 gulpfile.js를 다음 이름으로 바꾸자.
>
> > ![asdsadadawbfbcv](https://user-images.githubusercontent.com/46839654/69813425-88729a00-1235-11ea-8eca-4a54093163ed.png)
>
> 이제 다시 gulp dev를 입력해보면
>
> > ![asdsaadadasddasasas](https://user-images.githubusercontent.com/46839654/69813504-b0fa9400-1235-11ea-9f11-f7d9fa2298b2.png)
> >
> > 첫번째 줄에 babel을 사용한다고 적혀있고, 저번이랑 똑같이 dev라는 task가 없다고 함.
> >
> > 이게 바로 gulp 프로젝트를 시작하는 방법이다.

# Gulp 기본 문법

### gulp.src

> `gulp.src("파일 경로", [옵션])`
>
> gulp의 task를 실행 할 원본 파일을 지정한다.
>
> > ![src](https://user-images.githubusercontent.com/46839654/69894053-8e639a80-135d-11ea-982c-e8bf8e6fbc05.png)

### gulp.dest

> `gulp.dest("폴더 및 파일 경로", [옵션])`
>
> gulp의 task가 실행된 파일을 저장할 경로를 지정한다.
>
> > ![dest](https://user-images.githubusercontent.com/46839654/69894075-0a5de280-135e-11ea-9d53-9266abe02b99.png)

### gulp.series

> `gulp.series([func string])`
>
> 많은 수의 task를 개별 인수로 전달할 수 있다. 이전에 task를 등록한 경우 문자열을 사용할 수 있지만, 권장하지는 않는다.
>
> 구성된 작업이 실행되면 모든 작업이 순차적으로 실행됩니다. 한 작업에서 오류가 발생하면 후속 작업이 실행되지 않습니다.
>
> ![series](https://user-images.githubusercontent.com/46839654/69894127-9cfe8180-135e-11ea-8e87-2e57ed611d3e.png)

### gulp.parallel

> `gulp.parallel([task])`
>
> > ![parallel](https://user-images.githubusercontent.com/46839654/69894221-26628380-1360-11ea-83d6-d81792d1f4b0.png)
>
> 구성된 작업이 실행되면 모든 작업이 최대 동시성으로 실행됩니다. 한 작업에서 오류가 발생하면 다른 작업은 비 결정적으로 완료되거나 완료되지 않을 수 있습니다.

# Gulp pug

pug을 번들링 한다.

- 설치
  > npm i del
  >
  > > del : 폴더를 지워주는 패키지
  >
  > npm i gulp-pug -D
- gulpfile.babel.js
  > ![asdasdadawdawaw](https://user-images.githubusercontent.com/46839654/69814720-26fffa80-1238-11ea-9770-628156849bb5.png)
  >
  > > gulp.src() = 번들링 할 파일을 지정해준다. \*은 모든 파일, \*\*은 모든 폴더를 뜻한다.
  > >
  > > .pipe() = 파이프를 연결하면서 원하는 모양으로 만듭니다.
  > >
  > > gulp.dest() = 번들링 된 파일을 집어넣을 폴더를 지정.
  > >
  > > del = del([ ]) 안에 폴더들의 배열을 갖는다. 여기에 적힌 폴더들은 삭제된다.
  > >
  > > gulp.series([ ]) = 지정해둔 작업들을 집어넣어 순서대로 실행되게 한다.
  > >
  > > export 하는 것은 package.json에서 사용할 command만 해주면 된다. 만약 clean을 export 하지않으면 사용하지 못한다.
- pug files
  > templates/layout.pug
  >
  > > ![awdawdadaw](https://user-images.githubusercontent.com/46839654/69815544-e1443180-1239-11ea-96c1-12683efaae45.png)
  >
  > index.pug
  >
  > > ![asdaasasasdasddasassa](https://user-images.githubusercontent.com/46839654/69815545-e1dcc800-1239-11ea-88e3-5a4777f6751f.png)
- 실행
  > ![zxczxccczcxczcxzx](https://user-images.githubusercontent.com/46839654/69814721-26fffa80-1238-11ea-9cc8-43294875e9c7.png)
  >
  > 번들링이 끝나고 난 후
  >
  > > ![sdffsdsfdsdfsdf](https://user-images.githubusercontent.com/46839654/69815403-96c2b500-1239-11ea-81c6-db2f03bdb554.png)
  >
  > 변환된 html을 확인해보면
  >
  > > ![adawdkadakwkj](https://user-images.githubusercontent.com/46839654/69815180-23b93e80-1239-11ea-8cdc-7078c2464450.png)
  >
  > html 형식에 맞게 변환되어 있는 것을 확인할 수 있다.

---

# Gulp SASS

gulp-sass라는 멋진 플러그인으로 트랜스파일이 가능하다.

> npm i gulp-sass -D
>
> [npm link](https://www.npmjs.com/package/gulp-sass)
>
> > 하지만, 그 전에 `node-sass`를 설치해야 한다.
> >
> > 하나는 gulp랑 동작하는 것이고, 다른 하나는 node와 동작한다.
> >
> > 기본적으로 gulp-sass가 node-sass로 sass 파일을 전해준다.
> >
> > node-sass 설치 중 에러 발생시 `node_modules 폴더`를 삭제하고 다시 `npm i` 하면 된다.

### 사용법

> ![basicuse](https://user-images.githubusercontent.com/46839654/69849486-3034aa00-12c0-11ea-8856-fba55ae5e44c.png)
>
> > 공식문서를 참조하면, gulp와 gulp-sass를 불러오고 sass.compiler로 node-sass를 사용한다. 엄청 간단하다.

> ![asddsaasdasda](https://user-images.githubusercontent.com/46839654/69849852-252e4980-12c1-11ea-8cc3-086efdd946f1.png)
>
> > sass를 불러오고, sass.compiler를 설정해준다.

> ![aaaaaaaaa](https://user-images.githubusercontent.com/46839654/69851217-873c7e00-12c4-11ea-981a-f35089f84286.png)
>
> ![zxxzzxzx](https://user-images.githubusercontent.com/46839654/69850763-590a6e80-12c3-11ea-85bf-93b9f47f74bf.png)
>
> > routes와 task를 정의한다.
> >
> > `sass().on("error", sass.logError))`은 만약 여기서 에러가 발생한다면 sass만의 에러를 보여주는 것이다.
> >
> > sass의 에러는 좀 다르다. console을 죽이는 javascript 내에서의 에러를 원하는게 아님. `이런거 css에서 못찾겠어요` 같은 느낌이다.

> ![ccccccccccc](https://user-images.githubusercontent.com/46839654/69851299-b5ba5900-12c4-11ea-8916-88dd2bc7a728.png)
>
> > 이제 assets와 dev에 각각 넣어줍니다.
>
> ![zxzxxzzxxzxzxzxzx](https://user-images.githubusercontent.com/46839654/69851142-4d6b7780-12c4-11ea-903d-f824279d21fa.png)
>
> > `gulp dev`를 입력하면 잘 작동합니다.
>
> build 폴더를 확인해보면
>
> ![dddddddddddd](https://user-images.githubusercontent.com/46839654/69851366-e3070700-12c4-11ea-983d-8a5efd561118.png) > ![eeeeeee](https://user-images.githubusercontent.com/46839654/69851412-0467f300-12c5-11ea-9cf8-ae7998aaa90b.png)
>
> > 변환이 잘 되어있는 모습을 볼 수 있습니다.

- \_ (언더스코어)

  > scss파일에 `_`가 붙어있는 경우가 있는데, 이 밑줄은 sass한테 자기들을 compile 하진말고 사용만 하라고 알려주는 것이다.
  >
  > 만약 밑줄이 없다면 sass는 해당 파일명으로 css파일을 만들고 그걸 styles.css에 import할 것임. 그러면 결국 두 개의 파일을 얻기 때문에 밑줄을 선호한다.

- sass에서의 에러
  > 예를들어, 이 변수를 다른거로 바꿔보겠다.
  >
  > ![aaaaa](https://user-images.githubusercontent.com/46839654/69851692-9ff96380-12c5-11ea-9477-08298f2c2b29.png) > ![bbbbbb](https://user-images.githubusercontent.com/46839654/69851693-9ff96380-12c5-11ea-97dd-d03ea9f76dbb.png)
  >
  > 바꾸고 난 뒤, 다시 gulp dev를 실행하면
  >
  > ![cccccccc](https://user-images.githubusercontent.com/46839654/69851694-a091fa00-12c5-11ea-9a57-a3109710da1a.png)
  >
  > 이렇게 sass에서의 에러가 보이는 것을 확인할 수 있다.

**하지만, 최신 css를 사용하고 있다면 이것 만으로는 부족하다. 추가 설정을 더 해야한다.**

> gulp-autoprefixer라는 것을 설치해보자. 이 패키지는 기본적으로 우리가 작업한 코드를 알아듣지 못하는 구형 브라우저도 호환가능하게 만들어준다.
>
> > npm i gulp-autoprefixer -D
>
> 그런다음, import를 한다
>
> ![dddddd](https://user-images.githubusercontent.com/46839654/69851911-3af23d80-12c6-11ea-9f84-67b06096f3ad.png)
>
> 지금까지 한 작업들은 src 👉 pipe 👉 dest 총 3단계였는데, autoprefixer를 넣기위해 pipe를 하나 더 넣어야 한다.
>
> ![eeeeeee](https://user-images.githubusercontent.com/46839654/69852065-9fad9800-12c6-11ea-8a1a-15223e9edc6f.png)
>
> > autoprefixer에는 몇가지 옵션이 있다. 그 중 browsers:[ ] 는 코드를 얼마나 호환 가능하게 할지 정하는 것임.
> >
> > [문서](https://github.com/postcss/autoprefixer#options) 에 브라우저들이 있다. 예를들면
> >
> > ![fffffffff](https://user-images.githubusercontent.com/46839654/69852262-2c585600-12c7-11ea-87ad-d97e2e03cf3e.png)
> >
> > 이렇게 사용률이 5% 이상인, 미국에서 5% 이상인 브라우저 등등 목록이 여러개 있다.
> >
> > 위에서 사용한 `last 2 versions`는 모든 브라우저들의 최대 두단계 아래 버전까지 지원하겠다는 뜻임. (`이게 기본값임`)
>
> 이제 gulp dev 실행 후 결과를 확인해보면
>
> ![ggggggg](https://user-images.githubusercontent.com/46839654/69852530-d6d07900-12c7-11ea-9c54-cb0279895c7c.png)
>
> > `vh`, `flex` 등 최신 css 사용했고 `webkit`(chrome을 위한 호환성 처리)도 들어가있는 것을 볼 수 있다.
>
> 이게 `autoprefixer`다.
>
> 하지만, 이 아름다운 코드는 얘가 낼 수 있을 만큼의 속도가 나오지 않는다. 무슨 뜻이냐면, css파일들에 공백들이 들어가 있는데 이 공백 하나하나가 다 byte 용량들임.
>
> 그래서 지금부터 css를 최소화 할 것임. gulp-csso를 사용해서.
>
> 설치 및 import 해둔 `gulp-csso`를 pipe를 사용하여 추가한다.
>
> ![qqqqqqqqqqqqqq](https://user-images.githubusercontent.com/46839654/69852846-a76e3c00-12c8-11ea-9be9-d339915d1a0d.png)
>
> ![wwwwwwwwwwwwww](https://user-images.githubusercontent.com/46839654/69852974-ff0ca780-12c8-11ea-8a5e-38d0799a5594.png)
>
> > 옵션을 추가할 수 있지만, 아무것도 설정 안해도 충분하기 때문에 빈 상태로 놔둘 것임.
>
> 이제 다시 gulp dev를 실행하면
>
> ![yyyyyyyyyyyyyyyyyy](https://user-images.githubusercontent.com/46839654/69853075-3e3af880-12c9-11ea-9ca4-479019fee9d8.png)
>
> > 이렇게 공백이 하나도 없는 css파일을 볼 수 있다.
>
> **이렇게 pipe를 사용하면 원하는 모든 것을 다 넣을 수 있다. 차례대로 이어주기만 하면 된다.**

---

# Gulp Babel

Javascript를 다루기 위해서 할 것은 Javascript를 babel에서 실행 시키는 것인데, 그 다음 할 것은 Browserify에서 실행시키는 것이다.

### Browserify란?

> 개발자들이 브라우저에서 Node.js 스타일의 모듈을 사용하기 위한 오픈소스 JS 툴이다.
>
> 기본적으로 브라우저는 이런 문법을 이해 못한다.
>
> ![aaaa](https://user-images.githubusercontent.com/46839654/69893628-aa643d80-1357-11ea-983e-3515c227b673.png)
>
> > import나 export같은 것들
>
> Browserify는 이런 문법을 이해하도록 도와준다.
>
> 그러니 우리는 Browserify를 import하고, 그 Browserify 안에 Babel을 실행해야 한다. 이게 기본이다. 엄청 쉽다.

### 시작

> 먼저, gulp를 위한 browserify를 설치하자.
>
> `npm i gulp-bro`
>
> `npm i babelify`
>
> `npm i uglifyify`
>
> > [npm link](https://www.npmjs.com/package/gulp-bro)
>
> > gulp-browserify는 더이상 유지보수가 안되어 gulp-bro를 사용한다.
>
> 사용법을 보자
>
> ![bb](https://user-images.githubusercontent.com/46839654/69893680-6cb3e480-1358-11ea-8234-288e08fce373.png)
>
> > app.js를 가지고 browserify를 pipe로 연결하세요.. 네. 그 다음 저장할 위치를 지정하세요. 엄청 간단하다.
> >
> > 하지만 우리는 이와 동시에 js파일들을 변형해줘야 합니다.
> >
> > Browserify를 사용하지만, 그와 동시에 babelify도 사용해야 한다. 이렇게 해서 코드에 babel을 사용할 수 있다.
> >
> > 만약 React에서 사용할 거라면, react preset같은 걸 설치해줘야 한다.
> >
> > ![ccc](https://user-images.githubusercontent.com/46839654/69893704-e2b84b80-1358-11ea-88ea-168641d25aca.png)
> >
> > 지금은 하나 밖에 없지만, 프리셋이 더 들어간다.

### 설정

> ![dddd](https://user-images.githubusercontent.com/46839654/69893747-68d49200-1359-11ea-9020-4700cc0e30a8.png)
>
> > 먼저, 모듈을 import 해주고
>
> ![eeee](https://user-images.githubusercontent.com/46839654/69893794-ff08b800-1359-11ea-8c8c-58c9ce8a0fbf.png)
>
> > js 경로를 만들어 준다. 이렇게 안만들고 `gulp.src`에서 바로 접근해도 된다.
> >
> > js의 경우 main.js에 모든 js 모듈이 import 되어있는 상태로, 소스는 `main.js` 하나만 필요하다.
> >
> > 하지만 지켜봐야 하는 파일들은 모든 js파일이다.
>
> ![ffff](https://user-images.githubusercontent.com/46839654/69893821-5c9d0480-135a-11ea-8f12-af5ed10125f5.png)
>
> > 이제 task를 작성한다.
> >
> > `babelify.configure({})`의 key인 `presets`는 현재 `@babel/preset-env`로 사용중이기 때문에 preset-env로 적는다.
>
> ![ggg](https://user-images.githubusercontent.com/46839654/69893849-b6053380-135a-11ea-828f-9d01a95caec1.png)
>
> > 이제 dev 명령어로 사용하기 위해 적절한 위치에 js를 집어넣는다.

### 실행

> ![hhhh](https://user-images.githubusercontent.com/46839654/69893882-15fbda00-135b-11ea-83b3-af73b4db6a50.png)
>
> 코드를 확인해보자
>
> ![bbb](https://user-images.githubusercontent.com/46839654/69893912-77bc4400-135b-11ea-90cd-2a20e0109bd2.png)
>
> 이랬던게
>
> ![aa](https://user-images.githubusercontent.com/46839654/69893911-7723ad80-135b-11ea-8c23-05d50e96f51c.png)
>
> 구형코드로 트랜스파일과 난독화가 되었다. ~~그리고 엄청나게 압축이 되었다~~

---
