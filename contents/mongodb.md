- [MongoDB](#mongodb)
- [MongoDB 모델 만들고 데이터 삽입하기](#mongodb-%eb%aa%a8%eb%8d%b8-%eb%a7%8c%eb%93%a4%ea%b3%a0-%eb%8d%b0%ec%9d%b4%ed%84%b0-%ec%82%bd%ec%9e%85%ed%95%98%ea%b8%b0)
    - [Model](#model)
    - [body-parser](#body-parser)
    - [req](#req)
    - [데이터 삽입](#%eb%8d%b0%ec%9d%b4%ed%84%b0-%ec%82%bd%ec%9e%85)

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
  > >
  > > `const video = db.create({});` 👉 `res.redirect(/video/${video.id});`
  > >
  > > 이런 흐름으로 코드를 작성하면 된다. 중간에 에러를 잡아내야 한다면 `try-catch`를 사용한다.
  > >
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