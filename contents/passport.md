- [Passport](#passport)
    - [인증](#%ec%9d%b8%ec%a6%9d)
    - [구성](#%ea%b5%ac%ec%84%b1)
- [PassportLocalMongoose를 통한 회원가입](#passportlocalmongoose%eb%a5%bc-%ed%86%b5%ed%95%9c-%ed%9a%8c%ec%9b%90%ea%b0%80%ec%9e%85)
    - [설치](#%ec%84%a4%ec%b9%98)
    - [DB 설정](#db-%ec%84%a4%ec%a0%95)
    - [전략](#%ec%a0%84%eb%9e%b5)
    - [미들웨어](#%eb%af%b8%eb%93%a4%ec%9b%a8%ec%96%b4)
    - [라우트 핸들러](#%eb%9d%bc%ec%9a%b0%ed%8a%b8-%ed%95%b8%eb%93%a4%eb%9f%ac)
    - [로그아웃](#%eb%a1%9c%ea%b7%b8%ec%95%84%ec%9b%83)
    - [템플릿](#%ed%85%9c%ed%94%8c%eb%a6%bf)
    - [실행 결과](#%ec%8b%a4%ed%96%89-%ea%b2%b0%ea%b3%bc)

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