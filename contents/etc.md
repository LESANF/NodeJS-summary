- [템플릿에서 접근이 가능한 속성 locals](#%ed%85%9c%ed%94%8c%eb%a6%bf%ec%97%90%ec%84%9c-%ec%a0%91%ea%b7%bc%ec%9d%b4-%ea%b0%80%eb%8a%a5%ed%95%9c-%ec%86%8d%ec%84%b1-locals)
- [express static](#express-static)
- [fetch와 axios](#fetch%ec%99%80-axios)
    - [fetch](#fetch)
    - [axios](#axios)
- [express-flash](#express-flash)
    - [Requires](#requires)
    - [Usage](#usage)
    - [Add animation](#add-animation)
- [dotenv](#dotenv)
    - [사용법](#%ec%82%ac%ec%9a%a9%eb%b2%95)
- [AWS S3](#aws-s3)
    - [업로드를 위한 준비](#%ec%97%85%eb%a1%9c%eb%93%9c%eb%a5%bc-%ec%9c%84%ed%95%9c-%ec%a4%80%eb%b9%84)
    - [S3에 업로드](#s3%ec%97%90-%ec%97%85%eb%a1%9c%eb%93%9c)
- [CORS](#cors)

---

# 템플릿에서 접근이 가능한 속성 locals

- middleware.js
  > ![middleware-locals](https://user-images.githubusercontent.com/46839654/69619255-a8ac2880-107e-11ea-8d79-edf4d58edeab.png)

- main.pug
  > ![main-locals](https://user-images.githubusercontent.com/46839654/69619254-a8139200-107e-11ea-94ff-b5f0129e43db.png)

- app.js
  > ![home-locals](https://user-images.githubusercontent.com/46839654/69619253-a8139200-107e-11ea-80d4-d7c18ca7cce6.png)

- results
  > ![result-locals](https://user-images.githubusercontent.com/46839654/69619451-edd05a80-107e-11ea-8135-4ad038b8cd11.png)

res.render()의 인자는 (`템플릿 파일명`, `넘길 데이터`) 로 이루어 진다.

특정 템플릿에만 데이터를 넘기지만, `res.locals`는 전역적으로 데이터를 넘김.

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





# express-flash

이 모듈은 우리 홈페이지에 접속한 user에게 메시지를 보낼 수 있는 모듈이다.

임시적으로 html에 메시지를 추가해준다고 보면 된다.

주로 언제 사용하냐면, 글이 삭제되면 "deleted"라는 메시지, 로그인 비밀번호가 틀리면 "do not match" 라는 메시지 등을 보여주고 싶을 때 사용한다.

### Requires

npm i **express-flash**
> [express-flash](https://www.npmjs.com/package/express-flash)

npm i **cookie-parser** **express-session**

### Usage

![image](https://user-images.githubusercontent.com/46839654/71956308-2478c380-322e-11ea-8caa-800dc305cd4f.png)
> 우선 패키지들을 불러온다.

![image](https://user-images.githubusercontent.com/46839654/71956262-0743f500-322e-11ea-8e9f-a1c6b26eea1f.png)
> **pug**을 사용하고, 미들웨어로 **cookieParser**, **session**, **flash를** 사용했다.

![image](https://user-images.githubusercontent.com/46839654/71957280-acf86380-3230-11ea-943a-f10e4f40763a.png)
> 마지막으로 라우팅 과정에서 `req.flash(type, message)`를 작성한다.
>
> **type**에는 `"info"`, `"success"`, `"error"` 세 가지 종류가 있다.

![image](https://user-images.githubusercontent.com/46839654/71956764-576f8700-322f-11ea-91fa-deffa68ec4ff.png)
![image](https://user-images.githubusercontent.com/46839654/71956655-11b2be80-322f-11ea-8c1f-b6f3965100f3.png)
> pug을 작성한다.

여기까지 했다면 당신은 이 화면을 볼 수 있다.
> ![image](https://user-images.githubusercontent.com/46839654/71956737-445cb700-322f-11ea-8388-6202298be550.png)
![image](https://user-images.githubusercontent.com/46839654/71956796-69512a00-322f-11ea-88a2-3089393c6456.png)

이제 **/home**으로 접속하면 flash message는 나타나지 않는다. (해당 경로는 flash를 안보냈기 때문에)
> ![image](https://user-images.githubusercontent.com/46839654/71957444-1f694380-3231-11ea-862d-54e53c424a28.png)
![image](https://user-images.githubusercontent.com/46839654/71957447-2001da00-3231-11ea-819e-13b33f6ed49d.png)


### Add animation

지금까지 한 작업으로는 다음과 같은 질문을 할 수 있다.
> "왜 flash message인데 안사라지고 그대로 있나요?"
>
> "제가 생각한 flash message가 아닌 것 같아요"

다시 강조하지만 **express-flash**는 **임시적으로 HTML에 메시지를 추가해준다.**

그냥 HTML 태그일 뿐이고, 그래서 "/" 경로에만 div.message.info가 생긴 것이다.

이제 멋진 애니메이션을 추가해보자.

![image](https://user-images.githubusercontent.com/46839654/71958144-e205b580-3232-11ea-856a-164f52d3fa25.png)
![image](https://user-images.githubusercontent.com/46839654/71958217-14171780-3233-11ea-9724-f4ff5223ca8c.png)
> 템플릿에 mixin을 추가 해봤다.

![image](https://user-images.githubusercontent.com/46839654/71957702-d5cd2880-3231-11ea-98a0-e947f1798f67.png)
![image](https://user-images.githubusercontent.com/46839654/71957704-d665bf00-3231-11ea-8ef3-abef5dc7e262.png)
> style을 추가한다. **만약 sass를 사용한다면 Nesting 해도 좋다.**
>
> 여기서는 gif 캡쳐를 위해 width: 20%로 만들었는데, 실사용에서는 100%로 하면 된다.
>
> keyframes의 0-5%, 5-95%, 95-100%가 의미하는 바는 **user**에게 flash message같은 속임수를 주기 위해
>
> flash message가 생성되면 html의 보이지 않는 영역에서 부터 출발하여 기존 위치에 머무르고, 다시 위로 보낸다.
>
> **forwards**를 추가하지 않으면 **.flash-message__container**는 애니메이션이 끝난 후 html의 보이는 영역에 머무른다.
> 
> **만약 sass를 사용중이라면 다음과 같이 작성한다.**
>
> ![image](https://user-images.githubusercontent.com/46839654/71958378-812aad00-3233-11ea-8cf1-149789dc6624.png)

![image](https://user-images.githubusercontent.com/46839654/71957958-6572d700-3232-11ea-9977-3d5247054794.png)
> 처음부터 css로 작성된 것을 추가하든, 모듈번들러로 번들 되어진 css를 추가하든 자유다.

**결과물**

![1-min](https://user-images.githubusercontent.com/46839654/73276644-5b8a3580-422c-11ea-8864-d8c0774bdc9e.gif)
> 애니메이션을 적용해서 이제야 Flash message 다워졌다.
>
> `req.flash(1, 2)`가 적용된 경로에서만 **flash message**가 보여진다.

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

# CORS

**이 부분은 Node로 API 서버를 만들고 있지 않다면 넘어가도 좋다.**

CORS란 **Cross Origin Resource Sharing**의 약자이다. **현재 도메인과 다른 도메인으로 리소스가 요청될 경우**를 뜻한다.

보안 상의 이유로, 브라우저는 **CORS**를 제한하고 있다.

하지만 RESTful API를 기반으로 SPA를 만들게 되면 API 서버와 웹앱의 서버가 다를 수 있다. 이런 경우 CORS 제한이 걸린다.

이를 해결하기 위한 가장 간단한 방법은 **API 서버**의 **응답 헤더**를 변경하는 것이다.

만약 공공 API를 사용하는데, CORS가 걸리면 Express로 간단히 API 서버를 만든 뒤, 요청하면 된다.

**만약 당신이 API 서버를 만들었는데, 브라우저에서 CORS가 걸렸으면 세 가지의 헤더 설정을 해주면 된다.**

다음 코드는 내가 API 서버를 만들 때 사용한 설정이다.
> ![image](https://user-images.githubusercontent.com/46839654/72219804-5c18a000-358d-11ea-9ab5-d2a5f8f0e081.png)
> > **Access-Control-Allow-Origin** : 요청이 허용되는 URL을 Route 제외하고 작성, "*"은 모든 요청 허가
> >
> > **Acces-Control-Allow-Methods** : 요청이 허용되는 HTTP Method를 작성, 미포함된 Method는 거절, * 사용 불가
> >
> > **Access-Control-Allow-Headers** : 요청이 허용되는 HTTP Header 목록을 작성, 미포함된 Header는 사용불가, * 사용 불가

해당 API 서버는 토큰 인증 API 서버로, 토큰을 Headers로 받기 때문에 추가했다.

저렇게 설정한 뒤, 미들웨어 사용하듯이 사용하면 된다. (라우터 위에 해야한다)
> ![image](https://user-images.githubusercontent.com/46839654/72220020-b87cbf00-358f-11ea-8271-ddf23f77d723.png)

---