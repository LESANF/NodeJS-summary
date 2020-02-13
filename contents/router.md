- [라우터 Router](#%eb%9d%bc%ec%9a%b0%ed%84%b0-router)
    - [HTTP](#http)
    - [GET](#get)
    - [POST](#post)
    - [GET와 POST의 차이점](#get%ec%99%80-post%ec%9d%98-%ec%b0%a8%ec%9d%b4%ec%a0%90)
    - [app.js](#appjs)
    - [router.js](#routerjs)
    - [results](#results)

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