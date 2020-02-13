- [배포를 위해 서버 코드를 구형 코드로 변환](#%eb%b0%b0%ed%8f%ac%eb%a5%bc-%ec%9c%84%ed%95%b4-%ec%84%9c%eb%b2%84-%ec%bd%94%eb%93%9c%eb%a5%bc-%ea%b5%ac%ed%98%95-%ec%bd%94%eb%93%9c%eb%a1%9c-%eb%b3%80%ed%99%98)

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
> ![carbon (6)](https://user-images.githubusercontent.com/46839654/71782969-a052f000-3023-11ea-81a2-02b42575153b.png)
>
> ![image](https://user-images.githubusercontent.com/46839654/71460523-90e7d180-27ef-11ea-92c4-e1f89c09dd72.png)
>
> > 다시 강조하지만 `cross-env`는 신경쓰지 않아도 된다.

**배포 플랫폼**에서 `Linux`를 사용하는 경우 우리의 코드도 `UNIX`에 맞게 `start command`를 바꿔줘야 한다.

**Heroku**에 배포할 생각이라면 이정도 해두면 된다.
> ![carbon (7)](https://user-images.githubusercontent.com/46839654/71782975-c37d9f80-3023-11ea-9d81-ca5e5f066c41.png)

**템플리트 엔진**을 사용하였다면 `pug`의 `script태그 src`와 `link태그 href`도 고쳐줘야 한다.
> ![carbon (8)](https://user-images.githubusercontent.com/46839654/71782985-db552380-3023-11ea-942e-15596b5e9b06.png)
>
> `app.use("/static", express.static(path.join(__dirname, "static")));`이 적용된 상태다.

추가적으로 **프론트엔드 css/js**도 최신 문법이라면 **모듈번들러**를 통해서 변환된 서버 코드가 있는 `build` 폴더에 집어넣어줘야 한다.
> ![carbon (9)](https://user-images.githubusercontent.com/46839654/71782992-135c6680-3024-11ea-9d48-55553dd72a60.png)
>
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