### 오타 / 누락 / 내용 추가는 이슈 주세요.

- [1. Node.js란?](#NodeJS)
- [2. 개발환경 세팅](#프로젝트-시작하기)
- [3. 빠르게 서버 만들기](#express-서버-만들기)
- [4. 라우터](#라우터-Router)
- [5. 미들웨어](#미들웨어-Middleware)
- [5-1. Nodemon](#Nodemon)
- [5-2. multer](#Multer)
- [5-3. body-parser](#body-parser)
- [6. 템플릿 엔진](#템플릿-엔진-pug)
- [7. res.locals](#템플릿에서-접근이-가능한-속성-locals)
- [8. express.static](#express-static)
- [9. fetch / axios](#fetch와-axios)
- [10. MongoDB 기본 설정](#MongoDB)
- [10-1. MongoDB 데이터 삽입](#MongoDB-모델-만들고-데이터-삽입하기)
- [10-2. Passport란?](#Passport)
- [10-3. Passport-local-mongoose로 회원가입 만들기](#PassportLocalMongoose를-통한-회원가입)
- [11. 민감한 정보, dotenv로 가리자](#dotenv)
- [12. AWS S3](#AWS-S3)
- [13. 서버 코드를 구형 코드로 트랜스파일](#배포를-위해-서버-코드를-구형-코드로-변환)
- [14. Gulp 시작하기](#Gulp를-시작하는-법)
- [14-0 Gulp 기본문법](#Gulp-기본-문법)
- [14-1 Gulp_pug](#Gulp-pug)
- [14-2 Gulp_SASS](#Gulp-SASS)
- [14-3 Gulp_Babel](#Gulp-Babel)

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

1. Git 설치 및 세팅 [Git download](https://git-scm.com/)
   - > git config --list를 입력하면 현재 설정 값들을 볼 수 있다.
   - > git config --global `user.name` "**your name**"
   - > git config --global `user.email` "**your email**"
     >
     > > `공용컴퓨터에선 --global로 설정 X`
   - > git config --unset `config.name` (--global이 아닌 설정 삭제)
   - > git config --unset --global `config.name` (--global인 설정 삭제)
     > 단축 git command
     > git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
     >
     > > `git lg`를 입력하면 가독성 있게 보여준다. (`git log`는 동일하게 사용가능)
     >
     > git config --global alias.st status -> gir st (git status)
     >
     > > `git st`를 입력하면 `git status`와 같은 기능
2. Windows 10 개발자모드 활성화
   - > 설정 > 업데이트&보안 > 개발자 > 개발자모드
     >
     > > ![devenable2](https://user-images.githubusercontent.com/46839654/69611428-13566780-1071-11ea-9286-641ffed52c42.PNG)
   - > Windows 기능 > **리눅스 하위 시스템** 활성화
     >
     > > ![devenable](https://user-images.githubusercontent.com/46839654/69611424-12253a80-1071-11ea-88dd-88d3141f2cec.PNG)
3. NodeJS 설치 [Node download](https://nodejs.org/ko/)
   > 자동으로 `npm`이 설치됨.
   >
   > npm이란? `node package manager`이다. Node 프로젝트의 패키지를 관리한다.
   >
   > 설치가 끝나면 터미널에서 `npm -v`과 `node -v`를 입력 해보자.
4. VSC 설치 (텍스트 에디터) [VSC download](https://code.visualstudio.com/)
   > 확장프로그램 `Prettier 필수`
   >
   > > Prettier 설정
   > >
   > > ![amkiu](https://user-images.githubusercontent.com/46839654/69908458-752a1f00-142d-11ea-8870-c8e782bbc881.png)
   > >
   > > ![zzzd](https://user-images.githubusercontent.com/46839654/69908483-dbaf3d00-142d-11ea-9ef7-6e4fa63b260d.png)
   > >
   > > `"editor.formatOnSave": true` 추가
   >
   > VSC 내에서 터미널을 사용할 수 있는데, `cmd`, `bash(WSL)` 등등 설정해서 사용할 수 있다.
   >
   > > Windows 사용자라면 기본값으로 cmd가 적용되어 있다.
   >
   > 자신이 Windows 사용자이고, VSC의 기본 터미널을 바꾸고 싶다면 아래와 같이 하면 된다.
   >
   > > Microsoft Store에서 `Ubuntu`를 설치한다.
   > >
   > > ![ubuntu](https://user-images.githubusercontent.com/46839654/69894779-fae39700-1367-11ea-9e65-d3e397341e91.png)
   > >
   > > 설치가 끝나면 실행해서 잠시 기다린 다음, username과 password를 입력한다.
   > >
   > > 이건 Ubuntu지만 아무것도 설치되어있지 않기 때문에, `설정법`은 다른 개발 블로그들을 확인하자.
   > >
   > > `Ctrl` + `,`으로 VSC 설정을 연다. 그런 다음 `terminal.integrated.shell.windows`을 검색한다.
   > >
   > > cmd를 사용하는 경우 : "terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe"
   > >
   > > WSL을 사용하는 경우 : "terminal.integrated.shell.windows": "C:\\Windows\\System32\\bash.exe"

---

# 프로젝트 시작하기

### NPM 명령어

1. 콘솔에서 해당 경로 진입 후 `npm init` 입력
2. 정보 입력 후 마무리
3. 필요한 패키지 설치
   > ❗ **devDependencies에 설치된 패키지들은 배포 과정( build 후 )에서 삭제 됩니다.** ❗
   >
   > ❓ 전체적인 **배포 과정이 끝나면** 트랜스파일 되어진 코드로만 서버를 구동하기 때문에, **Slug Size를 줄이는 과정**입니다.
   >
   > ✅ **babel**, **nodemon**, **eslint**, **prettier**, **gulp**같은 개발에만 필요한 패키지는 **devDependencies**에 설치하는게 바람직 합니다.
   >
   > npm install `패키지 명` [ -D or -g ]
   >
   > > npm 패키지 문서를 보면 `--save(-dev)`이 추가된 것을 볼 수 있다.
   > >
   > > `--save`는 해당 패키지를 `dependencies` 항목에 추가한다. **생략해도 된다.**
   > >
   > > `--save-dev`는 해당 패키지를 `devDependencies` 항목에 추가한다. **-D를 사용하면 생략해도 된다**
   >
   > npm install `패키지` `패키지` `...`
   >
   > > **공백**으로 패키지를 **구분**하면 한번의 명령으로 **여러 패키지**를 설치할 수 있습니다.
   >
   > -D : devDependencies에 설치됨
   >
   > > 생략한 경우 dependencies에 설치됨
   >
   > -g : 전역으로 설치됨 (다른 프로젝트에도 적용)
   >
   > "`npm i`" 로 단축할 수 있다.
4. 패키지 삭제
   > npm uninstall "`해당 패키지 명`"
5. 스크립트

- 예약어 npm start
  > "start" : "node src/server.js" 설정 시
  >
  > > `npm start` 명령어로 시작
  >
  > ❗ **배포** 시에는 주로 `"start": "NODE_ENV=production node build/server"`를 입력합니다. ❗
- 그외 명령어
  > "dev:server" : "node src/server.js" 설정 시
  >
  > > `npm run dev:server` 명령어로 시작

1. 자주 사용하는 패키지
   - > Babel - `@babel/core`, `@babel/node`, `@babel/preset-env` ( **devDependencies에 설치한다** )
     - > Babel 설정
       >
       > > ![babel](https://user-images.githubusercontent.com/46839654/69611403-0a659600-1071-11ea-9fb2-fc748e2516e5.PNG) ![image](https://user-images.githubusercontent.com/46839654/71640106-25a66f80-2cc7-11ea-9ed0-d38c2fbfbd2a.png)
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

> **npm i express**
>
> [express 공식문서](https://expressjs.com/ko/)
>
> ![image](https://user-images.githubusercontent.com/46839654/71640156-14aa2e00-2cc8-11ea-8997-f881a9a12feb.png) > ![image](https://user-images.githubusercontent.com/46839654/71640160-2c81b200-2cc8-11ea-82bb-a1481768768e.png)

`res.send(expression)`는 문자열을 띄어주고, `res.render("템플릿", {data})`는 템플릿을 보여주고, `res.json(data)`는 json 형태로 data를 반환한다.

위의 코드는 **@Babel/preset-env**가 적용된 상태임. 적용하지 않으면 구형 자바스크립트를 사용해야함.

---

# 라우터 Router

### HTTP

`GET`과 `POST`로 넘어가기 전에 **HTTP 프로토콜**에 대해 알아보자.

> HTTP는 웹상에서 클라이언트와 서버 간에 요청/응답으로 데이터를 주고 받을 수 있는 프로토콜이다.
>
> 클라이언트가 HTTP 프로토콜을 통해 서버에게 요청을 보내면 서버는 요청에 맞는 응답을 클라이언트에게 전송한다.
>
> 이 때, HTTP 요청에 포함되는 HTTP 메소드는 서버가 요청을 수행하기 위해 해야할 행동을 표시하는 용도로 사용한다.

### GET

**서버로부터 정보를 조회하기 위해 설계된** 메소드다.

`GET`은 `request`를 전송할 때, 필요한 데이터를 `body`에 담지않고 `쿼리스트링`을 통해 전송한다.

`URL`의 끝에 `?`와 함께 **name**과 **value**로 쌍을 이루는 요청 파라미터를 쿼리스트링이라고 부른다.

만약 `요청 파라미터`가 여러 개이면 `&`로 연결한다.

> i.e. **localhost:4000/search?term=Larry&filter=age**
>
> 위와 같은 모양으로 `URL`에 `입력 form의 데이터`가 보여진다.

### POST

**리소스를 생성/변경하기 위해 설계된** 메소드다.

`GET`과 다르게 전송할 데이터를 HTTP 메시지의 `body`에 담아서 전송한다.

`body`는 길이의 제한없이 데이터를 전송할 수 있다. 그래서 `POST`는 대용량 데이터를 전송할 수 있다.

이처럼 `POST`는 데이터가 `body`로 전송되고 내용이 눈에 보이지 않아 `GET`보다 보안적인 면에서 안전하다고 느낄 수 있지만

`POST`도 개발자 도구에 들어가면 내용을 확인할 수 있기 때문에 **민감한 데이터는 반드시 암호화** 해야한다.

`POST`로 `request`를 보낼 때는 요청 헤더의 `Content-Type`에 `요청 데이터의 타입`을 표시해야 한다.

이 과정을 생략하면 서버는 내용이나 URL에 포함된 리소스로 데이터 타입을 유추한다.

만약 알 수 없는 경우에는 `application/octet-stream`으로 요청을 처리한다.

### GET와 POST의 차이점

`GET`은 동일한 요청과 동일한 응답이 돌아오고, `POST`는 동일한 요청과 응답은 항상 다를 수 있다.

이에 따라 `POST`는 서버의 상태나 데이터를 변경할 때 사용한다.

영상을 업로드하면 서버에 영상이 저장되고, 영상을 삭제하면 해당 데이터가 사라지는 등 서버의 데이터를 변경한다.

이처럼 `POST`는 **create**, **update**, **delete**에 사용할 수 있지만

`create`는 **POST**, `update`는 **PUT OR PATCH**, `delete`는 **DELETE**가 더 맞는 메소드라고 볼 수 있다.

### app.js

![router-app](https://user-images.githubusercontent.com/46839654/69612394-ee62f400-1072-11ea-94f5-121b8f539d73.png)

### router.js

![router-router](https://user-images.githubusercontent.com/46839654/69612395-eefb8a80-1072-11ea-9db3-90e992bb37b1.png)

> `/:id`는 파라미터 변수로, 예를들면 영화 id가 203인 그 영화을 보여줄 때 활용한다.
>
> **파라미터 변수 값**은 해당 라우터의 콜백 함수에서 `req.params`로 받을 수 있다.
>
> `const { id } = req.params;` OR `const { params : {id} } = req;` (Destructuring)

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

# Nodemon

`nodemon`은 프로젝트 폴더의 파일 변경이 감지되면 자동으로 서버를 재시작 하는 툴이다.

### 설치

> ![nodemon](https://user-images.githubusercontent.com/46839654/70028855-0c87a180-15e9-11ea-9d2e-d26a42cdf4c3.png)
>
> > 전역으로 설치해도 좋고, 개발자용으로 설치해도 좋다.

### 사용법

> ![nodemonusege](https://user-images.githubusercontent.com/46839654/70029037-7f911800-15e9-11ea-8193-677c803114a2.png)
>
> > 기본적으로는 `nodemon 'your server file'` 이다.

### 설정

> ![nodemonpackage](https://user-images.githubusercontent.com/46839654/70029174-d8f94700-15e9-11ea-8480-f5d10513e55f.png)
>
> > 설정에는 1. **nodemon.json을 이용한 방법**, 2. **command line을 이용한 방법** 두가지가 있다.
> >
> > --config 파일을 지정하거나 `nodemon.json`이 감지되면 `package.json`에서의 설정은 무시된다.
>
> 기본적으로 babel-node와 nodemon을 사용한다고 하면 아래와 같이 설정한다.
>
> > ![nodemonpackagejson](https://user-images.githubusercontent.com/46839654/70029578-c5021500-15ea-11ea-87fc-fb5a619f1171.png)
>
> 부가적인 설정 (ignore, exec, delay, etc.) 들은 [nodemon npm](https://www.npmjs.com/package/nodemon)에서 확인해보자.

---

# Multer

Multer는 파일 업로드를 위해 사용되는 multipart/form-data 를 다루기 위한 node.js 의 미들웨어 입니다. 효율성을 최대화 하기 위해 busboy 를 기반으로 하고 있습니다.

**주: Multer는 multipart (multipart/form-data)가 아닌 폼에서는 동작하지 않습니다.**

> npm i multer
>
> > [사용법](https://github.com/expressjs/multer/blob/master/doc/README-ko.md)

### 활용

> 일단 간단하게 텍스트 파일을 읽어들이게 만들어 보겠다.
>
> [fs 문서](https://nodejs.org/api/fs.html)
>
> form 입력을 사용하기 때문에, bodyParser를 사용하였다.
>
> ![12](https://user-images.githubusercontent.com/46839654/70031719-38a62100-15ef-11ea-9bde-de6497477e68.png)
>
> > multer를 import해서 upload 안에 파일을 저장할 위치를 지정해준다.
> >
> > 그리고 파일이 업로드 되어 서버로 보내지는 시점에
> >
> > `multer({dest: "./uploads/"}).single("input의 name")` 을 삽입하면 된다.
> >
> > single()은 **req.file**에 파일이 저장된다.
>
> ![5435435](https://user-images.githubusercontent.com/46839654/70031760-4f4c7800-15ef-11ea-8e70-a760ed16f163.png)
>
> > 파일이나 이미지를 서버로 전송할 때 form의 enctype을 multipart/form-data로 준다.
>
> ![566456](https://user-images.githubusercontent.com/46839654/70031771-5a070d00-15ef-11ea-8c0d-244a66f5fbb2.png)
>
> > render를 통해 받은 데이터로 화면을 꾸민다.
>
> ![1241312](https://user-images.githubusercontent.com/46839654/70032274-7788a680-15f0-11ea-9111-f26891f9c1db.png) > ![21321asdas](https://user-images.githubusercontent.com/46839654/70032405-c7676d80-15f0-11ea-9742-8408abdd916b.png)
>
> > 서버에 저장된 파일명은 무작위로 생긴다.

---

# body parser

**request**의 본문을 해석해주는 **미들웨어**다.

보통 `form`의 데이터나 `AJAX request`의 데이터를 처리한다.

express 4.1.6.0 버전부터 **body-parser**의 일부 기능이 **express**에 내장 되었다. 어떻게 사용하는지 보자.

![carbon (3)](https://user-images.githubusercontent.com/46839654/71643492-d29bdf00-2cfd-11ea-831d-7018b3cddc9f.png)

> urlencoded의 설정값 extended가 **false**면 `querysring` 모듈을 사용하여 쿼리스트링을 해석하고
>
> **true**면 `qs` 모듈을 이용하여 쿼리스트링을 해석한다.
>
> `qs`는 npm 패키지고, `querystring`은 내장 모듈이다. `qs`는 `querystring` 모듈의 기능을 조금 더 확장한 모듈이다.

하지만 `body-parser`가 필요한 경우가 있다.

`body-parser`는 **JSON**과 **URL-encoded** 형식의 본문 외에도 `Raw`, `Text` 형식의 본문을 추가로 해석할 수 있다.

**body-parser**를 통해 받은 폼 데이터는 `req.body`에 저장된다.

> ![image](https://user-images.githubusercontent.com/46839654/71476813-4d5e8900-282a-11ea-8834-1822d6e1142c.png) > ![image](https://user-images.githubusercontent.com/46839654/71476847-7aab3700-282a-11ea-9855-51040775fc6f.png)

만약 **URL-encoded** 형식으로 `id=12312&pw=1231221`을 본문으로 보낸다면 위와 같이 **req.body**에 저장된다.

**body-parser**가 모든 본문을 해석해주는 건 아니다. `multipart/form-data`같은 폼을 통해 전송된 데이터는 해석하지 못한다.

---

# 템플릿 엔진 pug

[Express와 함께 템플리트 엔진 사용](https://expressjs.com/ko/guide/using-template-engines.html)

### pug 설치

> npm i pug
>
> > [pug 설정 및 문법](https://pugjs.org/api/getting-started.html)

### app 설정

![image](https://user-images.githubusercontent.com/46839654/71762321-33e7cc00-2f11-11ea-8468-46b177f55960.png)

> pug의 default 폴더명은 "`views`"이다. 바꿀 수 있음.
>
> > \_\_dirname은 현재 디렉터리를 표시하고, path.join은 매개변수를 잇는다(join).

### pug 문법

#### layout && include

레이아웃 기능을 지원하여 중복을 제거할 수 있다.

또한, include로 페이지에 페이지를 끼워넣을 수 있다.

> ![main-pug](https://user-images.githubusercontent.com/46839654/69617586-c1ffa580-107b-11ea-87d1-ec054e949b84.png)
> ![header-pug](https://user-images.githubusercontent.com/46839654/69617581-c1670f00-107b-11ea-8cb4-3d8d2116df0d.png)
> ![home-pug](https://user-images.githubusercontent.com/46839654/69617584-c1670f00-107b-11ea-819a-9c052420e252.png)
> ![result-pug](https://user-images.githubusercontent.com/46839654/69617589-c1ffa580-107b-11ea-964b-05183b0d6e95.png)

#### link css && script

번들링 되어진 css와 js는 레이아웃으로 만들어진 main.pug에 다음과 같이 불러오면 된다.
> ![image](https://user-images.githubusercontent.com/46839654/71766293-c607c880-2f41-11ea-925b-e7d4c5d46128.png)

#### mixin

**React**를 해봤는가? 그렇다면 **Component** 개념을 알고 있는가? 그렇다면 여기서도 컴포넌트를 사용할 수 있다.

사용법은 간단하다. mixin을 만든 다음, mixin을 include하고 `+mixinName({})`으로 사용하면 된다.

값을 넘길 때는 props 넘기듯이 `propName: data`로 **+mixinName** 첫번째 인자인 객체에 작성해주면 된다.

> ![image](https://user-images.githubusercontent.com/46839654/71762261-a1472d00-2f10-11ea-8052-526196ced62d.png)
> ![image](https://user-images.githubusercontent.com/46839654/71762272-b754ed80-2f10-11ea-93d7-b987031d37fa.png)
> ![image](https://user-images.githubusercontent.com/46839654/71762280-c5a30980-2f10-11ea-8d5f-afd26ce68184.png)
> ![image](https://user-images.githubusercontent.com/46839654/71762284-d2bff880-2f10-11ea-8f41-c9b11317ae02.png)
> ![image](https://user-images.githubusercontent.com/46839654/71762291-e79c8c00-2f10-11ea-97f2-f031b0042429.png)

### IF ~ ELSE

**템플릿 언어**이긴 하지만 약간의 프로그래밍적인 기능을 지원한다.
> ![image](https://user-images.githubusercontent.com/46839654/71762400-0e0ef700-2f12-11ea-962a-63e4d71bd83b.png)

위의 코드는 `"/"`에 접근하면 서버는 API를 fetching 하는데 (app 설정 참조)

**res.render**로 받은 user가 존재하면 **.container**를 보여준다.

만약 느낌표를 붙인다면 **존재하지 않을 때**로 의미가 바뀐다.
> ![image](https://user-images.githubusercontent.com/46839654/71762440-837ac780-2f12-11ea-9728-67333ae534f9.png)

✅ **TIP** 회원가입 혹은 로그인 실패할 시 render로 변수를 하나 만든 뒤 넘겨서 템플릿에서는 해당 변수의 유무에 따라 메시지를 출력할 수도 있겠다. (flash message를 사용해도 좋다)

### 반복문 (배열)

배열에 한해서 `map()`과 같은 기능을 구현할 수 있다.

먼저, 이 user는 다음의 posts 배열을 가지고 있다.
> ![image](https://user-images.githubusercontent.com/46839654/71762551-c2f5e380-2f13-11ea-8ac7-a18621d29578.png)
> ![image](https://user-images.githubusercontent.com/46839654/71762552-c38e7a00-2f13-11ea-8933-e45918b3807f.png)

배열을 하나씩 읽어서 **title**과 **description**만 뽑아 보겠다.
> ![image](https://user-images.githubusercontent.com/46839654/71762578-3a2b7780-2f14-11ea-9c88-e4598776819d.png)
> ![image](https://user-images.githubusercontent.com/46839654/71762583-47e0fd00-2f14-11ea-96f5-5f7101596b34.png)

❗ 꼭 **item**이 아니더라도 다른 이름을 사용할 수 있다. ❗

![image](https://user-images.githubusercontent.com/46839654/71762591-6ba44300-2f14-11ea-848d-053e339ccfa9.png)

다만 이름을 바꿀거면 다음과 같이 바꿔야 한다.

![image](https://user-images.githubusercontent.com/46839654/71762609-a908d080-2f14-11ea-8913-0f2d985f188c.png)

`map(item => item)` 처럼 **인자**명은 일치해야 한다.

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

  > ![image](https://user-images.githubusercontent.com/46839654/71640290-ac108080-2cca-11ea-94e3-3851d6519318.png) > ![image](https://user-images.githubusercontent.com/46839654/71640266-5340e800-2cca-11ea-8234-49e564560cde.png)
  >
  > > app.use()의 첫번째 인자, 경로를 생략하면 모든 경로에 static이 적용된다.
  >
  > **아래와 같이 URL로 접근이 가능하다.**
  >
  > > ![image](https://user-images.githubusercontent.com/46839654/71640262-30163880-2cca-11ea-8874-a1ef51e9777f.png)

- 사용 예제

  > ![pug static](https://user-images.githubusercontent.com/46839654/69711162-ecb53100-1143-11ea-8bd0-48c86a6bc13a.png)
  >
  > ![pugjsstatic](https://user-images.githubusercontent.com/46839654/69711163-ed4dc780-1143-11ea-8f3d-6286f545aac6.png)
  >
  > > static 폴더가 모든 경로에서 기본값으로 지정되었기 때문에 파일을 지정할 때 이런 형식으로 사용한다.

- 더 많은 정보
  > [Express에서 정적 파일 제공](https://expressjs.com/ko/starter/static-files.html)

---

# fetch와 axios

먼저 위에 두개를 이해하기 위해선 **Ajax**를 알아야 한다.

Ajax는 `Asynchronous JavaScript and XML`의 약자이다. 해석하면 비동기적인 웹 앱을 만들기 위한 웹개발 기법이다.

요즘은 JSON으로 많이 사용하기 때문에 Ajaj라고 불러야 할지 모른다.

이를 도입했을 때의 장점

- 페이지 이동없이 고속으로 화면을 전환할 수 있다
- 서버 처리를 기다리지 않고, 비동기 요청이 가능하다.
- 수신하는 데이터 양을 줄일 수 있고, 클라이언트에게 처리를 위임할 수 있다.

### fetch

> Ajax를 구현하기 위한 최신 기술인 fetch API를 사용할 수 있음.
>
> 사용하기에 앞서, **Promise**라는 개념을 익혀야 한다.
>
> `fetch('주소', 설정객체).then(콜백).catch(콜백)` 👉 fetch 요청 후의 return 값이 promise 객체이다.
>
> > 기본적인 구조이다. 요청을 보낼 주소를 입력하고, 설정객체에 GET, POST 등의 메소드, 보낼 데이터 등을 넣을 수 있다.
> >
> > [fetch 문서](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Fetch%EC%9D%98_%EC%82%AC%EC%9A%A9%EB%B2%95)
> >
> > **then** 에서 응답 response 객체를 받고 catch에선 요청에 대한 에러를 받는다.
>
> 사용 예제
>
> > ![carbon](https://user-images.githubusercontent.com/46839654/69917345-12c23480-14a8-11ea-9bb9-35de50cd848d.png)
> >
> > 이런 식으로 함수를 만들 수 있다.

### axios

> [axios npm](https://www.npmjs.com/package/axios)
>
> 기존의 fetch보다 더 다양한 기능을 쓰기위해 `axios`를 사용한다.
>
> axios는 npm 패키지이다.
>
> 여러 API를 불러오는데, URL이 겹치는 부분이 있다면 아래처럼 사용할 수 있다.
>
> > ![dawddnbfg](https://user-images.githubusercontent.com/46839654/69918199-77828c80-14b2-11ea-815b-13949d64dee0.png)
> >
> > `axios.create`로 기본 URL을 설정하고 get()에서 `baseURL + 나머지 URL`을 입력할 수 있다.
> >
> > 사용하는 API에서 params를 지원하는 경우 위처럼 활용이 가능하다.
>
> 백엔드를 구축하였고, 서버 내부의 API를 활용하는 경우
>
> > 아래는 프론트엔드의 js파일이다.
> >
> > ![carbon (2)](https://user-images.githubusercontent.com/46839654/69917445-93356500-14a9-11ea-9c1b-0cf1e9a94da8.png)
> >
> > 아래는 백엔드 API의 라우터 부분이다.
> >
> > ![carbon (3)](https://user-images.githubusercontent.com/46839654/69917498-13f46100-14aa-11ea-8342-056c8934129f.png)
> >
> > `ADD_COMMENT = "/api/:videoId/comment"`
> >
> > ![carbon (4)](https://user-images.githubusercontent.com/46839654/69917499-15258e00-14aa-11ea-98ea-e3309c4e2cba.png)
> >
> > 전체적으로 살펴보면, 프론트의 axios에서 보낸 POST에 data (comment)가 있다.
> >
> > 서버는 이를 `파라미터 변수 id` 와 `axios를 통해 받은 data를 req.body.comment` 그리고 `passport로 생성된 req.user` 로 가져와서 처리를 한다.
> >
> > API 처리 중 에러가 발생하면 status 코드를 400 (클라이언트 에러) 내보내고, 결과적으로 response를 끝낸다.
> >
> > 백엔드에서 처리가 다 끝나고 return 받은 status 코드가 200 (정상)이면 댓글을 클라이언트 페이지에 비동기로 생성하는 코드다.

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
  > > NodeJS를 위한 Object modeling.
  > >
  > > [공식문서](https://mongoosejs.com/docs/guide.html)
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

form 입력 데이터를 백엔드에서 받으려면 **body-parser** 가 필요하다.

express에 내장된 body-parser를 사용하려면 `5.3` 항목을 참조해보자.

> npm i body-parser
>
> [body-parser](https://www.npmjs.com/package/body-parser)
>
> > ![bodyParser](https://user-images.githubusercontent.com/46839654/69716933-7407a200-114e-11ea-94f5-3b25ea8fa719.png)
>
> `app.use(bodyParser...)`는 pug 설정 밑에 적도록 하자.

### req

req, res, next 중 `req`는 `request`의 약어인데, console.log(req)를 하면 전체적인 요청들을 확인할 수 있다. 그 중에서 form 데이터를 받기 위해 req.body를 활용할 것이다.

❗ POST METHOD는 **HTTP Message의 Body**에 데이터를 담아서 보냅니다. ❗

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
  > > `const video = db.create({});` 👉 `res.redirect(/user/${user.id});`
  >
  > > 이런 흐름으로 코드를 작성하면 된다. 중간에 에러를 잡아내야 한다면 `try-catch`를 사용한다.
  >
  > > `const { email, password } = req.body;` 👉 const { **템플릿의 input에 설정해둔 name** } = req.body
- 결과
  > ![UserCreatedconsole](https://user-images.githubusercontent.com/46839654/69717740-f6449600-114f-11ea-8ac0-6d68c2b566a7.png)
  >
  > > 정상적으로 DB에 등록이 된 것을 확인할 수 있다.
  > >
  > > MongoDB는 자동으로 `_id(Object Id)`가 생기는데, 이를 통해 데이터 관리를 체계적으로 할 수 있다.
  > >
  > > 예를들면, `db.users.findOne({id: object._id})`

---

# Passport

[passport documentation](http://www.passportjs.org/docs/downloads/html/)

**passport**는 **Node.js**의 인증 미들웨어다. 인증 요청이라는 단일 목적을 제공하도록 설계되어 있습니다.

모듈을 작성할 때, 캡슐화는 필수이므로 **passport**는 모든 기능을 앱에 위임한다.

이렇게 분리한 관계는 코드를 깔끔하게 유지하게 도와주고, **passport**를 쉽게 통합할 수 있게 해줍니다.

일반적으로 user는 **username**과 **password**를 사용하여 로그인 하는데,

SNS의 등장으로 **facebook** 또는 **카카오톡**과 같은 **OAuth 공급자**를 사용한 **Single sign-on**(SSO)이 널리 사용되는 인증방법이 되었다.

**API**를 노출하는 서비스는 접근을 보호하기 위해 **토큰 기반 자격 증명**이 필요하다.

**Passport**는 각 앱마다 고유한 인증 요구사항이 있음을 인식하는데, `전략`이라는 **인증 메커니즘**은 **개별 모듈로 패키지** 되어진다.

따라서 앱은 불필요한 종속성을 만들지 않고 사용할 **Strategy**(전략)을 선택할 수 있다.

### 인증

요청 인증은 `passport.authenticate()`를 호출한 다음, 사용할 **Strategy**를 지정만 해주면 된다. 매우 간단하다.

❗ **Strategy**는 route에서 strategy를 사용하기 전에 먼저 구성해야 합니다.

**Example**

> ![image](https://user-images.githubusercontent.com/46839654/71638195-eebb6400-2c9c-11ea-9e1b-32ce9aff86ae.png)
>
> ![image](https://user-images.githubusercontent.com/46839654/71638267-fc71e900-2c9e-11ea-81d0-b20e1c9024fb.png)
>
> > token은 신경쓰지 않아도 된다. [nodeMongoAPI](https://github.com/Kunune/nodeMongoAPI)를 만드는 중 예시로 사용한 것이다.
>
> ![image](https://user-images.githubusercontent.com/46839654/71638274-1ad7e480-2c9f-11ea-9b00-816bc4adda8f.png)
>
> > 인증에 성공하면 **다음 핸들러**가 실행되고, **req.user** 속성이 **인증된 user**로 설정된다.

`passport.authenticate()`가 성공적으로 로그인 되면 additional route handlers들이 호출된다.

만약, 인증에 **실패**하면 기본적으로 **401 Unauthorized** 상태로 응답하며 router handler는 호출되지 않는다.

> ![image](https://user-images.githubusercontent.com/46839654/71638249-72298500-2c9e-11ea-8845-e0d2bb465f78.png)

**Redirects**

이렇게 `passport.authenticate()` 실행 후 **additional route handler**를 실행하는 것 외에 **템플릿 엔진**을 사용해서 프론트를 작성할 경우

> ![image](https://user-images.githubusercontent.com/46839654/71638319-e4e73000-2c9f-11ea-977b-09ab58c9cd58.png)
>
> > **이 경우**에는 `Redirection` 옵션이 기본 동작을 **무효화** 시킵니다.

위와 같이 **인증 성공 시 redirect 경로**와 **인증 실패시 redirect 경로**를 설정해줄 수 있다.

**Disable Sessions**

인증에 성공하면 `Passport`는 **req.session.passport.user**에 user를 저장한다.

> ![image](https://user-images.githubusercontent.com/46839654/71638570-da7c6480-2ca6-11ea-8db3-fcd588ef9a1f.png) > ![image](https://user-images.githubusercontent.com/46839654/71638572-f1bb5200-2ca6-11ea-8bbc-f7764b4505c7.png)

이는 브라우저를 통해 웹앱에 접근하는 일반적인 사용자 시나리오에 유용하다.

하지만 경우에 따라 세션 지원이 필요없다. API 서버같은 경우가 대표적인 예다.

**API서버**는 일반적으로 각 요청과 함께 자격 증명을 제공해야 하는데, 이 경우 **session**을 **false**로 설정하여 세션을 안전하게 비활성화 할 수 있다.

아래와 같이 작성하면 **기본값**으로 `session: true`가 된다.

> ![image](https://user-images.githubusercontent.com/46839654/71638415-c2a2e180-2ca2-11ea-8f4f-54853a4e6d89.png)
>
> ![image](https://user-images.githubusercontent.com/46839654/71638425-072e7d00-2ca3-11ea-811e-8396b5565081.png) > ![image](https://user-images.githubusercontent.com/46839654/71638426-085faa00-2ca3-11ea-94e2-70c895008333.png)
>
> > 지금 이 경우에는 API 서버기 때문에 **세션 관련 설정**을 모두 **제거**했다.
> >
> > 그래서 **직렬화 실패**와 `passport.initialize()`를 사용하라고 에러가 나왔다.

이제 `session: false`를 설정해보자

> ![image](https://user-images.githubusercontent.com/46839654/71638436-668c8d00-2ca3-11ea-9130-7aa93e113f35.png)
>
> ![image](https://user-images.githubusercontent.com/46839654/71638448-c2efac80-2ca3-11ea-8241-15a64f11edfe.png)
>
> > **session**을 **false**로 비활성화 해주니 세션 관련 **에러**가 나오지 않는다.

### 구성

**Strategies**

passport는 전략을 사용해 요청을 인증한다. 전략이란 username && password, OAuth를 사용한 위임된 인증 또는 OpenID를 사용한 연합 인증의 범위다.

passport에 요청을 인증하도록 요청하기 전에 앱에서 사용하는 전략을 구성해야 한다.

전략 및 구성은 `use()`를 통해 제공된다. 예를들어, 다음은 **JWT token**를 사용한 인증에 사용한다.

> ![carbon](https://user-images.githubusercontent.com/46839654/71642706-df670580-2cf2-11ea-86e4-3de860ba8a7d.png)

**Verify Callback**

전략에는 콜백 확인 작업이 필요하다. 이 작업의 목적은 자격 증명을 가지고 있는 user를 찾는 것이다.

passport는 요청을 인증할 때, 요청에 포함된 자격 증명을 구문 분석한다.

그런 다음, 해당 자격 증명을 매개변수로 사용하여 verify callback을 호출한다. (이 경우 payload)

인증 정보가 유효하면 verify callback의 `done`이 인증 된 user가 포함된 passport를 제공한다.

![carbon (4)](https://user-images.githubusercontent.com/46839654/71643503-00812380-2cfe-11ea-8fba-5fe469482b52.png)

비밀번호가 일치하지 않는 등 로그인 정보가 유효하지 않은 경우

인증 실패를 표시하기 위해 user 대신 false를 사용하여 `done`을 호출한다.

![carbon (5)](https://user-images.githubusercontent.com/46839654/71643517-23133c80-2cfe-11ea-88c4-129f3df11506.png)

실패 사유를 표시하기 위해 추가적인 정보가 담긴 메시지를 제공할 수 있다.

이것은 user에게 다시 시도하라는 flash message를 표시하는데 유용하다.

![carbon (6)](https://user-images.githubusercontent.com/46839654/71643519-33c3b280-2cfe-11ea-8923-fda63802fa0c.png)

마지막으로 자격 증명을 확인하는 동안 **예외**가 발생한 경우 (예제 : 서버 에러, DB 접근 불가 등)

Node 방식으로 **error**와 함께 `done`을 호출해야 한다.

![carbon (7)](https://user-images.githubusercontent.com/46839654/71643528-4b9b3680-2cfe-11ea-8768-ee0eaa40b964.png)

두가지 인증 실패 사례가 발생할 수 있다. **서버 예외**는 error가 null이 아닌 값으로 설정된다. **인증 실패**는 서버가 정상 작동하는 자연 조건이다.

Strategy를 구성한 다음, `passport.authenticate("인증 방식", options)` 구문을 실행하면

성공적으로 로그인 되었을 경우 `req.user`에 logged user의 정보가 들어가서

`passport.authenticate(..., {successRedirect: "/", failureRedirect: "/login"})`와 같이 리디렉션 하거나

매개변수로 (req, res, next(optional))를 갖는 `additional route handler`로 다른 작업을 하거나

`passport.authenticate(..., ..., (error, user) => {})`와 같이 **Custom Callback**을 사용할 수 있다.

**Middleware**

express를 기반으로 하는 웹앱(템플릿 엔진 사용)의 경우 **passport**를 초기화하는 `passport.initialize()` 미들웨어가 필요하다.

웹에서 페이지가 이동해도 로그인을 유지 시키고 싶으면 `passport.session()`도 사용해야 한다.

다음은 session에 로그인 정보를 저장하기 위한 application settings 이다.

![carbon (2)](https://user-images.githubusercontent.com/46839654/71643480-99636f00-2cfd-11ea-8c1d-304310dc0603.png)

(아래 Sessions와 같이 봐야함)

`passport.initialize()`은 **passport.serializeUser**를 실행하여 loggedUser의 id만 session에 직렬화 한다.

정리하면 `passport.serializeUser()`가 실행되면 **req.session.passport.user**에 usernameField로 설정된 DB 필드가 들어간다.

`passport.session()`은 **passport.deserializeUser**를 실행하여 최소한의 정보를 가지고 있는 **req.session.passport.user**에서

사용자를 식별할 수 있는 key로 DB 조회 후 얻은 **user**를 `req.user`로 삽입한다.

**Sessions**

일반적인 웹앱에서 사용자를 인증하는 데 사용되는 자격 증명은 로그인 요청 중에만 전송된다.

인증에 성공하면 브라우저에 설정된 쿠키를 통해 세션이 설정되고 유지된다.

이후의 각 요청에는 자격 증명이 아니라 세션을 식별하는 고유한 쿠키가 포함된다.

로그인 세션을 지원하기 위해 Passport는 session과 **user**를 serialize 및 deserialize 한다.

![carbon (1)](https://user-images.githubusercontent.com/46839654/71643452-38d43200-2cfd-11ea-9173-ad92a663ab67.png)

이 예에서는 세션 내에 데이터의 양을 작게 유지하면서 user.id만 세션에 serialize 되어진다.

후속 요청이 수신되면 user.id는 사용자를 찾는 데 사용되며 이 사용자는 **req.user**로 복원된다.

만약 세션을 사용하지 않는다면 `passport.initialize()`와 `passport.session()` 그리고 `express-session`은 제외해도 좋다.

---

# PassportLocalMongoose를 통한 회원가입

보통 passport로 **local** 로그인을 구현할 때, **passport-local**을 사용한다.

하지만 당신이 **mongoDB**와 **Node.js**, **Passport**를 사용한다면 다양한 기능이 있는 패키지를 사용할 수 있다.

바로 `passport-local-mongoose`다. 다양한 기능을 지원하고, 연결도 매우 간편해졌다.

### 설치

> npm i `passport`
>
> > [passport offical link](http://www.passportjs.org/)
>
> npm i `express-session` `connect-mongo` `cookie-parser`
>
> > [express-session](https://www.npmjs.com/package/express-session)
> >
> > [connect-mongo](https://www.npmjs.com/package/connect-mongo)
> >
> > [cookie-parser](https://www.npmjs.com/package/cookie-parser)
>
> npm i `passport-local-mongoose`
>
> > [passport-local-mongoose](https://github.com/saintedlama/passport-local-mongoose)

### DB 설정

먼저, User Schema를 생성한다. 그런 다음, User Schema에 **plugin**을 사용한다.

❗ **password field**를 따로 만들 필요는 없다. **plugin**에서 제공하는 Salt 암호화를 사용할 예정이다.

> ![image](https://user-images.githubusercontent.com/46839654/71663471-b9943c00-2d98-11ea-9bf4-41e320cf8ef3.png)
>
> > import 되어진 `passport-local-mongoose`를 UserSchema에 플러그인을 사용한다.
> >
> > UserSchema에만 passport-local-mongoose 플러그인을 사용하면 된다.
> >
> > 주의사항이 있다면 `UserSchema.plugin(passportLocalMongoose, option)`을 적어줘야 하는데
> >
> > option 중 **usernameField**는 설정하지 않으면 **기본 값**이 **username**이 된다.
> >
> > **usernameFiled**란 로그인할 때, ID 혹은 username, email로 입력받을 필드를 뜻 한다.
> >
> > 만약 **email**이나 다른 unique한 필드로 설정하고 싶다면 `{usernameField: "field name"}`를 option에 적어주면 된다.

### 전략

다음으로 사용할 전략을 `passport.use()`로 설정해주면 된다.

다만 다른 passport strategy들과 다른 점이 있다면 `passport-local`이 아닌 `User.createStrategy()`을 사용한다.

> ![image](https://user-images.githubusercontent.com/46839654/71664339-fd3c7500-2d9b-11ea-855b-ee2389fd958e.png)
>
> ![adwadaw](https://user-images.githubusercontent.com/46839654/69728902-acb47500-1168-11ea-9f1e-c3b190397c95.png)
>
> `serializeUser`와 `deserializeUser`에 대한 설명은 passport 항목의 sessions를 참조해보자.
>
> 여기에서 사용하는 것은 **그 과정**을 단축해둔 것이다.
>
> 👇 만약 passport-local-mongoose를 `사용하지 않는다면` 아래처럼 작성해야 한다. 👇
>
> ![image](https://user-images.githubusercontent.com/46839654/71666903-41cd0e00-2da6-11ea-9fa0-50c7d9e61472.png) > ![image](https://user-images.githubusercontent.com/46839654/71666850-0d595200-2da6-11ea-8d05-de9bc8efa01b.png)

### 미들웨어

다음은 passport 문서에서 제공하는 페이지 변경 시에도 로그인을 유지 시키기 위한 필수 미들웨어 목록이다.

다시 강조하지만 session을 사용하지 않는다면 관련 미들웨어는 사용하지 않아도 된다.

> ![carbon (2)](https://user-images.githubusercontent.com/46839654/71643480-99636f00-2cfd-11ea-8c1d-304310dc0603.png)
>
> > **express-session**과 **cookieParser**를 설치해야 한다.
> >
> > 추가적인 본문을 해석하려면 **body-parser**를 설치하면 된다.
>
> ![adwadaw](https://user-images.githubusercontent.com/46839654/69731784-d3c17580-116d-11ea-9909-c782587466db.png)
>
> > **18~ 30줄**은 passport-local과 session을 사용하기 위한 필수 설정임.
> >
> > **session의 secret은 암호화 문자열이다. 복잡하고 길어질 수록 좋다.**
> >
> > **passport.initialize()**, 👉 passport 모듈을 초기화한다.
> >
> > **passport.session()** 👉 session을 처리하는 이 두가지를 꼭 잊지말고 넣어줘야 한다. (공식문서 참조)
> >
> > **connect-mongo** : 서버가 재시작 되면 세션 정보가 사라지기 때문에 DB에 세션을 저장한다.
> >
> > 여기에서 설정 가능한 항목들을 확인해보자. [connect-mongo](https://www.npmjs.com/package/connect-mongo)
>
> 로그인 세션이 DB에 저장되면 이런 모양을 띈다.
>
> ![vbnds](https://user-images.githubusercontent.com/46839654/69908411-35166c80-142c-11ea-9166-83eba87c3d32.png)

### 라우트 핸들러

이제 POST로 로그인 폼 데이터를 받으면 해당 user를 찾아서 로그인 시켜줘야 한다.

❗ **로그인 전에 회원가입부터 시켜야 한다.** ❗

> ![image](https://user-images.githubusercontent.com/46839654/71666116-f107e600-2da2-11ea-8eeb-d399d74865ec.png)
>
> > passport-local-mongoose에 의해 제공되는 `db.register({userObject}, password)` 는 비밀번호를 salt로 암호화해서 숨긴다.
> >
> > ❗ **실제로 스키마에도 비밀번호를 만들지 않았다** ❗

로그인 시키기 위해 다음과 같이 코드를 짤 수 있다.

> ![image](https://user-images.githubusercontent.com/46839654/71666135-01b85c00-2da3-11ea-854d-42164d9c308a.png)

👇 **passport 공식 문서에서는 다양한 로그인 방법을 제공한다.** 👇

> ![image](https://user-images.githubusercontent.com/46839654/71445176-e58d3d00-275a-11ea-9611-b82e8ba98b9a.png)
>
> > `Authenticate request`는 `passport.authenticate()`에서 전략을 호출과 지정하면 끝날 정도로 간단하다.
> >
> > 기본적으로 인증이 실패하면 `Passport`는 **401 Unauthorized** 상태로 응답하며 **추가 경로 핸들러**는 호출되지 않음.
> >
> > 인증이 성공하면 **다음 핸들러**가 호출되고 `req.user`는 인증된 `user`로 설정이 된다.
>
> ![qws](https://user-images.githubusercontent.com/46839654/69907977-68083280-1423-11ea-90af-856747553045.png)
>
> > 로그인 작업이 완료되면 `user`는 `req.user`에 할당된다.
> >
> > **passport.authenticate** 미들웨어가 `req.login()`을 자동으로 호출한다.
> >
> > 이 기능은 회원가입할 때 주로 사용하며 `req.login()`하는 동안 새로 등록한 `user`를 자동으로 로그인 시킬 수 있다.
>
> ![image](https://user-images.githubusercontent.com/46839654/71445135-7adc0180-275a-11ea-8d68-a6ad9bebdeaf.png)
>
> > **redirection**은 일반적으로 요청을 인증한 후에 실행된다.
> >
> > 위와 같이 작성하게 되면 **redirect** 옵션이 기본 동작보다 먼저 실행된다. 인증에 성공하면 홈 페이지로 이동하고, 실패하면 로그인 페이지로 다시 이동한다.

### 로그아웃

> ![globalRouter](https://user-images.githubusercontent.com/46839654/69732025-429ece80-116e-11ea-8ccb-d10520f45687.png)

passport에 의해 `req.logout()`이 제공된다.

> ![aqw](https://user-images.githubusercontent.com/46839654/69907965-4909a080-1423-11ea-88f4-544972e87a7d.png)

### 템플릿

템플릿을 간단하게 만들어 보았다.

> ![home](https://user-images.githubusercontent.com/46839654/69732911-d58c3880-116f-11ea-8b63-2a29a3d7c579.png)

### 실행 결과

최초 접속 시 화면

> ![a](https://user-images.githubusercontent.com/46839654/69733282-74b13000-1170-11ea-9693-eea150c3cbe5.png)

회원가입

> ![h](https://user-images.githubusercontent.com/46839654/69733143-3287ee80-1170-11ea-8d93-c528584f49fd.png)

로그인

> ![b](https://user-images.githubusercontent.com/46839654/69733310-7ed32e80-1170-11ea-8e89-ecf6a0821c75.png)
>
> > res.locals에 의해 **req.user 객체**가 보여진다.
> >
> > ![carbon](https://user-images.githubusercontent.com/46839654/71666633-1ac20c80-2da5-11ea-9488-cfdae61ff942.png)

---

# dotenv

> github 등에 코드를 업로드 하게되면 자신의 API key, DB주소 및 계정 등 보여지지 말아야 할 것들이 올라가는 경우가 있다.
>
> 이런 상황을 위해 만들어진 패키지로, 사용법은 매우 간단하다.
>
> npm install `dotenv`
>
> > [npm link](https://www.npmjs.com/package/dotenv)

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

# AWS S3

S3이란 **Amazon Simple Storage Service**(Amazon S3)의 약자다. AWS의 수많은 서비스 중 하나다.

단어 그대로 간단한 저장공간 서비스다. 이것이 어떤 서비스냐면 **파일을 업로드**할 수 있는 서비스다.

영상, 텍스트, 실행파일, 이미지 등 뭐든 업로드할 수 있다.

이제 외부 파일 저장 서비스를 사용해야 하는 이유를 알아보자.

1. 서버에 유저의 파일을 저장하면 그것이 바이러스일 수 있고, 서버를 망가뜨릴 수 있다.
2. 많은 서버를 필요로 할 수 있다. 트래픽이 많아진다면.
3. 만약 아시아, 유럽, 북미에 여러 서버를 둘 경우에 같은 파일을 3 곳에 두는 걸 원치 않을 것이다. (돈도 돈이지만 엄청 피곤함)

이제 사용해야 하는 이유를 느꼈다면 AWS에 가입을 해보자.

AWS는 가입일 부터 1년간 **Free Tier**의 **12개월 무료** 서비스를 사용할 수 있다.

만약 유료로 사용한다 하더라도 매우 저렴한 편이다. 당신의 서버에 직접 저장소를 구입하는 것과 비교하면 말이다.

다음은 12개월 무료로 제공되는 것 중에 **S3**의 설명이다.

> ![image](https://user-images.githubusercontent.com/46839654/71759386-a942a500-2eef-11ea-8ab3-9d25e4e0663c.png)
>
> > AWS 신규 고객에게는 1년 동안 매달 5GB의 Amazon S3 스탠다드 스토리지, 20,000건의 Get 요청, 2,000건의 Put 요청, 15GB의 데이터 수신, 15GB의 데이터 송신 혜택이 제공됩니다.

✅ **IAM user에 S3 Full Access 권한을 주는 것과 버킷을 생성하는 과정은 구글링을 해보도록 하자.**

❗ **user access key와 secret key는 보안정책 상 해당 페이지를 떠나면 다시는 볼 수 없기에 메모를 해둬야 한다.** ❗

### 업로드를 위한 준비

dotenv 항목에서 설명한 `.env` 파일에 AWS KEY를 입력 후 저장

❗ **절대 AWS KEY를 외부에 노출 시키면 안됩니다. 요금 폭탄을 맞을 수 있음.** ❗

> ![carbon (3)](https://user-images.githubusercontent.com/46839654/71759515-77cad900-2ef1-11ea-85ee-541a55343ad7.png)

패키지 설치

> npm i multer-s3 aws-sdk
>
> > [multer-s3](https://www.npmjs.com/package/multer-s3) || [aws-sdk(software-development-kit)](https://www.npmjs.com/package/aws-sdk)

패키지 로드

> ![carbon (1)](https://user-images.githubusercontent.com/46839654/71759486-fecb8180-2ef0-11ea-87bc-82f22d60d0cc.png)

설정

> ![image](https://user-images.githubusercontent.com/46839654/71759542-e3ad4180-2ef1-11ea-803a-5951f1ccb02d.png)
>
> > 먼저, aws.s3의 설정을 해줘야 한다. **accessKeyId**, **secretAccessKey**, **region**이 있다.
> >
> > **region**은 ![image](https://user-images.githubusercontent.com/46839654/71759558-2ec75480-2ef2-11ea-8f60-c3632aee6fb1.png) 여기에 적힌 그대로 적으면 된다.
> >
> > 그 다음, multer 안에 storage 속성이 있다. 이 속성의 기본값은 **Node.js 파일 시스템**인데 S3으로 바꾼다는 뜻이다.
> >
> > storage 속성의 값을 **multer-s3**으로 사용하고, 이 **multer-s3** 안에 만들어둔 **s3**, **acl(access list)**, **bucket** 속성을 입력한다.
> >
> > **acl**은 다음을 참조한다.
> >
> > ![image](https://user-images.githubusercontent.com/46839654/71759632-536ffc00-2ef3-11ea-9504-abbe1e1207d5.png)
> >
> > **bucket**은 S3 Management Console 보이는 **Bucket Name**을 입력한다.

### S3에 업로드

우선, 파일을 업로드 하는 라우터에 export로 내보낸 multer를 끼워넣는다.

> ![carbon (5)](https://user-images.githubusercontent.com/46839654/71759702-04769680-2ef4-11ea-81df-feef70f33d23.png)

업로드 하기 전에 `req.file`이 어떤 객체를 반환할지 콘솔로 찍어보겠다.

> ![image](https://user-images.githubusercontent.com/46839654/71759713-515a6d00-2ef4-11ea-9412-606284b08080.png) > ![image](https://user-images.githubusercontent.com/46839654/71759766-6edc0680-2ef5-11ea-9bb9-22ec4b510b21.png)
>
> > 볼 수 있듯이, **location** 속성에 파일 접근이 가능한 AWS 주소가 있다.

S3 콘솔을 가보자.

> ![image](https://user-images.githubusercontent.com/46839654/71759800-00e40f00-2ef6-11ea-9654-2e595614a986.png)
>
> > 정상적으로 업로드 된 것을 볼 수 있다.

이제 DB에 저장된 fileURL로 파일을 불러올 수 있다.

> ![image](https://user-images.githubusercontent.com/46839654/71759817-7223c200-2ef6-11ea-8c58-496c2cf0a389.png)

---

# 배포를 위해 서버 코드를 구형 코드로 변환

AWS 혹은 Heroku에 배포할 때에는 최신 문법으로 작성된 Node server 코드를 트랜스파일 해줘야 한다.

> `npm i @babel/cli -D`
>
> > [babel-cli doc](https://babeljs.io/docs/en/babel-cli)

설치를 다 했으면 아래와 같이 `scripts`를 작성하자.

> ![image](https://user-images.githubusercontent.com/46839654/71459772-68aaa380-27ec-11ea-903a-b387a6ddc8ed.png)
>
> > `build:server`는 `src 폴더`를 `babel` 하는데, `--out (내보내는 형태)`는 `-dir (directory, 폴더)`로 `build 폴더`를 만들어서 집어넣겠다는 의미다.
> >
> > **다른 형태로 내보내고 싶다면 문서를 참조해보자.**

우선, 현재 서버 구성은 이렇다.

> ![image](https://user-images.githubusercontent.com/46839654/71459908-eff81700-27ec-11ea-8a89-1ec09587b29e.png)

이제 `build:server`를 실행해보자.

> ![image](https://user-images.githubusercontent.com/46839654/71459938-174ee400-27ed-11ea-864b-d0b3590b1b13.png) > ![image](https://user-images.githubusercontent.com/46839654/71459963-2df53b00-27ed-11ea-80ca-7ead3918f091.png)
>
> > `build` 폴더가 생겼다.

결과물을 보도록 하자.

> 아래와 같은 최신 문법의 코드가
>
> > ![image](https://user-images.githubusercontent.com/46839654/71460017-6eed4f80-27ed-11ea-8bdb-9362d51ee30c.png)
>
> 정상적으로 트랜스파일 되었다.
>
> > ![image](https://user-images.githubusercontent.com/46839654/71460019-6f85e600-27ed-11ea-9f63-02e32fbd83e1.png)

그렇다면 트랜스파일 되어진 `build/server.js`로 서버를 구동해보자.

> ![image](https://user-images.githubusercontent.com/46839654/71460091-c25f9d80-27ed-11ea-96a6-bc4bb0e08779.png) > ![123212132](https://user-images.githubusercontent.com/46839654/71460134-ec18c480-27ed-11ea-982a-881b7642a56f.gif)
>
> > 정상 작동한다.

배포할 때에는 `NODE_ENV`를 설정해줘야 한다.

실제 배포하는 것은 아니기 때문에 `cross-env(윈도우에서 환경 설정이 안되는 경우 사용)`를 사용했다.

    "start": "cross-env NODE_ENV=production node build/server.js"

> ![image](https://user-images.githubusercontent.com/46839654/71460523-90e7d180-27ef-11ea-92c4-e1f89c09dd72.png)
>
> > 다시 강조하지만 `cross-env`는 신경쓰지 않아도 된다.

**배포 플랫폼**에서 `Linux`를 사용하는 경우 우리의 코드도 `UNIX`에 맞게 `start command`를 바꿔줘야 한다.

**Heroku**에 배포할 생각이라면 이정도 해두면 된다.

    "start": "NODE_ENV=production node build/server.js"

**템플리트 엔진**을 사용하였다면 `pug`의 `script태그 src`와 `link태그 href`도 고쳐줘야 한다.

    link(rel="stylesheet", href="/static/styles.css")

    script(src="/static/main.js")

> `app.use("/static", express.static(path.join(__dirname, "static")));`이 적용된 상태다.

추가적으로 **프론트엔드 css/js**도 최신 문법이라면 **모듈번들러**를 통해서 변환된 서버 코드가 있는 `build` 폴더에 집어넣어줘야 한다.

    "scripts": {
    "dev:server": "nodemon --exec babel-node src/init.js --delay 2 --ignore '.scss' --ignore 'static' ",
    "dev:assets": "cd src && cross-env WEBPACK_ENV=development webpack -w", 👉 src로 이동한 후, 개발모드로 webpack-watch 모드 실행
    "build:assets": "cd src && cross-env WEBPACK_ENV=production webpack", 👉 src 이동 후, 배포모드로 webpack 실행
    "build:server": "babel src --out-dir build", 👉 src 폴더를 build 폴더에 트랜스파일
    "copyAll": "cp -R 'src/static' 'build' && cp -R 'src/views' 'build'", 👉 src/static와 src/view를 build 폴더로 복사
    "build": "npm run build:server && npm run build:assets && npm run copyAll", 👉 build command에 모두 실행되게 설정
    "tunnel": "ngrok http 4000",
    "start": "NODE_ENV=production node build/init.js" 👉 NODE_ENV가 'production(배포)'모드로 서버 실행
    }

> 위와 같이 작성하면 되는데, **주의사항**이라면 **배포 플랫폼**이 **Linux**를 사용한다면 위와 같이 **UNIX Command**를 사용해야 한다.
>
> 맥이나 리눅스로 작업하지 않고, `윈도우`로 처음부터 `WSL`을 사용하지 않았다면, 먼저 `window command`로 작성해두고 `UNIX Command`로 바꾸면 된다.

**다음은 실제 heroku build log다.**

![carbon (9)](https://user-images.githubusercontent.com/46839654/71643554-8ef5a500-2cfe-11ea-9e04-c72cba411272.png)

이렇게 `git push heroku master`를 실행하면 실행 순서가

패키지 다운로드 👉 **build** command 실행 👉 개발자 모듈 제거 👉 압축 👉 배포로

최종적으로 build 되어진 directory에서 `npm start`로 서버를 실행한다.

위에서도 적었지만, **babel**은 서버만 트랜스파일 하기 때문에, 그 외 **템플릿**은 폴더 째로 복사해주고 **scss / js**는 모듈번들러를 통해서 변환한 후 build directory로 복사 해줘야 한다.

---

# Gulp를 시작하는 법

gulp는 Fractal Innovations과 깃허브 오픈 소스 커뮤니티의 오픈 소스 자바스크립트 툴킷으로, 프론트엔드 웹 개발의 스트리밍 빌드 시스템로 사용된다.

### 모듈번들러

![adwadawdaw](https://user-images.githubusercontent.com/46839654/69810217-be605000-122e-11ea-92a3-98c3700bcc89.png)

> 모듈로 이루어진 scss와 front-end js파일을 각각 하나의 파일로 묶어주면서 구형 브라우저에 지원되게 코드를 트랜스파일 해준다.

### 설치

> npm i `gulp -D`
>
> > [Official gulp API](https://gulpjs.com/docs/en/getting-started/quick-start)
> >
> > [npm gulp link](https://www.npmjs.com/package/gulp)

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

---

# Gulp 기본 문법

### gulp.src

> `gulp.src("파일 경로", [옵션])`
>
> gulp의 task를 실행 할 원본 파일을 지정한다.
>
> ![src](https://user-images.githubusercontent.com/46839654/69894053-8e639a80-135d-11ea-982c-e8bf8e6fbc05.png)

### gulp.dest

> `gulp.dest("폴더 및 파일 경로", [옵션])`
>
> gulp의 task가 실행된 파일을 저장할 경로를 지정한다.
>
> ![dest](https://user-images.githubusercontent.com/46839654/69894075-0a5de280-135e-11ea-9d53-9266abe02b99.png)

### gulp.watch

> `gulp.watch("경로", task)`
>
> `경로`에 속한 파일들이 `변경`되면 두번째 인자, callback으로 다시 `task`를 실행한다.
>
> ![watch](https://user-images.githubusercontent.com/46839654/69894694-57de4d80-1366-11ea-854e-7d222078f83d.png)

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
> 구성된 작업이 실행되면 모든 작업이 최대 동시성으로 실행됩니다. 한 작업에서 오류가 발생하면 다른 작업은 비 결정적으로 완료되거나 완료되지 않을 수 있습니다.
>
> ![parallel](https://user-images.githubusercontent.com/46839654/69894221-26628380-1360-11ea-83d6-d81792d1f4b0.png)

# Gulp pug

pug을 번들링 한다.

- 설치
  > npm i del
  >
  > > del : 폴더를 지워주는 패키지
  > >
  > > [del API](https://www.npmjs.com/package/del)
  >
  > npm i gulp-pug -D
  >
  > > [gulp-pug API](https://www.npmjs.com/package/gulp-pug)
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
