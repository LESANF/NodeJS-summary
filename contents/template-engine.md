- [템플릿 엔진 pug](#%ed%85%9c%ed%94%8c%eb%a6%bf-%ec%97%94%ec%a7%84-pug)
    - [pug 설치](#pug-%ec%84%a4%ec%b9%98)
    - [app 설정](#app-%ec%84%a4%ec%a0%95)
    - [pug 문법](#pug-%eb%ac%b8%eb%b2%95)
      - [layout && include](#layout--include)
      - [link css && script](#link-css--script)
      - [mixin](#mixin)
    - [IF ~ ELSE](#if--else)
    - [반복문 (배열)](#%eb%b0%98%eb%b3%b5%eb%ac%b8-%eb%b0%b0%ec%97%b4)

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