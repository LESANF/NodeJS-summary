- [express 서버 만들기](#express-%ec%84%9c%eb%b2%84-%eb%a7%8c%eb%93%a4%ea%b8%b0)

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