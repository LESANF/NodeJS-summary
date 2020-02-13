- [미들웨어 Middleware](#%eb%af%b8%eb%93%a4%ec%9b%a8%ec%96%b4-middleware)
    - [middleware.js](#middlewarejs)
    - [router.js](#routerjs)
    - [app.js](#appjs)
    - [results](#results)
  - [>](#blockquoteblockquote)
- [helmet](#helmet)
    - [사용법](#%ec%82%ac%ec%9a%a9%eb%b2%95)
- [Nodemon](#nodemon)
    - [사용법](#%ec%82%ac%ec%9a%a9%eb%b2%95-1)
    - [설정](#%ec%84%a4%ec%a0%95)
- [Multer](#multer)
    - [활용](#%ed%99%9c%ec%9a%a9)
- [morgan](#morgan)
- [body parser](#body-parser)

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
> 
---

# helmet

`npm i helmet`
> [helmet](https://www.npmjs.com/package/helmet)

사용해야 하는 이유
> [프로덕션 환경의 Express를 위한 보안 우수 사례](https://expressjs.com/ko/advanced/best-practice-security.html)

### 사용법

GraphQL server안에 express를 활용했는데, `express.use`만 보면 된다.

NODE_ENV=production일 때만 helemt을 사용하고, morgan을 combined로 사용하는 코드다.

> import helmet from "helmet"
>
> ![image](https://user-images.githubusercontent.com/46839654/73847488-b98ccd80-4869-11ea-8133-2db0efae6242.png)


---

# Nodemon

`npm i nodemon -D`
> [nodemon](https://www.npmjs.com/package/nodemon)

`nodemon`은 프로젝트 폴더의 파일 변경이 감지되면 자동으로 서버를 재시작 하는 툴이다.


### 사용법

기본적으로는 `nodemon 'your server file'` 으로 사용을 한다.

i.e. `nodemon src/server.js`

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

# morgan

`npm i morgan`
> [morgan](https://www.npmjs.com/package/morgan)

서버가 받는 http request를 콘솔에 표현해주는 미들웨어다.

이게 없으면 GET / POST / PATCH / DELETE 등의 http request를 볼 수 없다.

✅ 주로 개발할 때는 `dev`, 배포할 때는 `combined, common`을 사용한다.

가능한 설정으로는 5개가 있다.
> ![image](https://user-images.githubusercontent.com/46839654/73846047-26529880-4867-11ea-91f1-10c3744fbb93.png)

1. dev
   > ![image](https://user-images.githubusercontent.com/46839654/73846121-513cec80-4867-11ea-8010-7ad99a630f4c.png)
2. short
   > ![image](https://user-images.githubusercontent.com/46839654/73846185-6e71bb00-4867-11ea-9f7d-43058550cad6.png)
3. tiny
   > ![image](https://user-images.githubusercontent.com/46839654/73846233-85b0a880-4867-11ea-9273-cd3663565728.png)
4. common
   > ![image](https://user-images.githubusercontent.com/46839654/73846567-14252a00-4868-11ea-9f18-5ba213c0872a.png)
5. combine
   > ![image](https://user-images.githubusercontent.com/46839654/73846715-5484a800-4868-11ea-985b-4e5a184b4855.png)

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