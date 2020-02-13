- [Gulp를 시작하는 법](#gulp%eb%a5%bc-%ec%8b%9c%ec%9e%91%ed%95%98%eb%8a%94-%eb%b2%95)
    - [모듈번들러](#%eb%aa%a8%eb%93%88%eb%b2%88%eb%93%a4%eb%9f%ac)
    - [설치](#%ec%84%a4%ec%b9%98)
    - [폴더 구조](#%ed%8f%b4%eb%8d%94-%ea%b5%ac%ec%a1%b0)
    - [package.json](#packagejson)
    - [Babel을 이용한 Gulp](#babel%ec%9d%84-%ec%9d%b4%ec%9a%a9%ed%95%9c-gulp)
- [Gulp 기본 문법](#gulp-%ea%b8%b0%eb%b3%b8-%eb%ac%b8%eb%b2%95)
    - [gulp.src](#gulpsrc)
    - [gulp.dest](#gulpdest)
    - [gulp.watch](#gulpwatch)
    - [gulp.series](#gulpseries)
    - [gulp.parallel](#gulpparallel)
- [Gulp pug](#gulp-pug)
- [Gulp SASS](#gulp-sass)
    - [사용법](#%ec%82%ac%ec%9a%a9%eb%b2%95)
- [Gulp Babel](#gulp-babel)
    - [Browserify란?](#browserify%eb%9e%80)
    - [시작](#%ec%8b%9c%ec%9e%91)
    - [설정](#%ec%84%a4%ec%a0%95)
    - [실행](#%ec%8b%a4%ed%96%89)

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