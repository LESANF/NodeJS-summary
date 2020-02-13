- [NPM 명령어](#npm-%eb%aa%85%eb%a0%b9%ec%96%b4)
- [Smart NPM scripts](#smart-npm-scripts)

---

# NPM 명령어

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
   > >
   > > ❗ 터미널에서 바로 `tsc`, `gulp` 등의 명령어를 사용하고 싶다면 -g로 설치
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

# Smart NPM scripts

`npm`이나 `yarn`은 똑똑해서 우리가 **build**를 호출하면 **prebuild** 👉 **build** 👉 **postbuild** 순서대로 호출한다.

짐작하는 것처럼 **prebuild**는 build 이전, **postbuild**는 build 후에 실행된다.

우선, 다음과 같이 설정했다.
> ![image](https://user-images.githubusercontent.com/46839654/72252032-02be7880-3642-11ea-8e1a-97220c9dfa17.png)
> > **역슬래시 2개**는 npm에게 window directory 구분자를 알려주기 위함임. UNIX사용, 배포 시에는 정상적으로 / 사용.
> >
> > **prebuild** : build directory 생성 후, prebuild.js를 build로 copy
> >
> > **build** : src/server.js를 트랜스파일 후 build directory로 copy
> >
> > **postbuild** : src/postbuild.js를 build directory로 copy

**npm run build** 명령을 실행한다.
> ![1-min (1)](https://user-images.githubusercontent.com/46839654/73276297-cf780e00-422b-11ea-8f90-2d62b5dbafdb.gif)
> ![image](https://user-images.githubusercontent.com/46839654/72253276-86796480-3644-11ea-82d1-b34b8659ea53.png)
> > npm run build 명령만 실행했는데 `prebuild`, `build`, `postbuild` 세 개 모두 실행된 것을 볼 수 있다.

이건 배포할 때 매우 유용하다.

예를들면, GraphQL build 작업을 하는데 src를 babel 돌리면 graphql 파일들은 옮겨지지가 않는다.

이런 경우 **postbuild**를 사용하여 graphql 파일들을 copy할 수 있다.

❗ `build` 외에도 **start** script도 **prestart**, **start**, **poststart**를 사용할 수 있다. ❗

---