- [NodeJS 개발환경 만들기](#nodejs-%ea%b0%9c%eb%b0%9c%ed%99%98%ea%b2%bd-%eb%a7%8c%eb%93%a4%ea%b8%b0)
    - [개발환경](#%ea%b0%9c%eb%b0%9c%ed%99%98%ea%b2%bd)

---

# NodeJS 개발환경 만들기

### 개발환경

1. Git 설치 및 세팅 [Git download](https://git-scm.com/)
   > user.name과 user.email을 --global 혹은 local로 설정해야 한다.
   >
   > 방법은 [여기](https://github.com/Kunune/Git-summary)를 참조.
2. Windows 10 개발자모드 활성화
   - > 설정 > 업데이트&보안 > 개발자 > 개발자모드
     >
     > > ![image](https://user-images.githubusercontent.com/46839654/71971886-ed66da00-324e-11ea-8cbd-d2b0d7d4ab6c.png)
   - > Windows 기능 > **리눅스 하위 시스템** 활성화
     >
     > > ![image](https://user-images.githubusercontent.com/46839654/71971785-aed11f80-324e-11ea-8484-f96f876f9c29.png)
3. NodeJS 설치 [Node download](https://nodejs.org/ko/)
   > 자동으로 `npm`이 설치됨.
   >
   > npm이란? `node package manager`이다. Node 프로젝트의 패키지를 관리한다.
   >
   > 설치가 끝나면 터미널에서 `npm -v`과 `node -v`를 입력 해보자.
4. VSC 설치 (텍스트 에디터) [VSC download](https://code.visualstudio.com/)
   > 확장프로그램 `Prettier 필수`
   >
   > > Prettier 설정
   > >
   > > ![amkiu](https://user-images.githubusercontent.com/46839654/69908458-752a1f00-142d-11ea-8870-c8e782bbc881.png)
   > >
   > > ![zzzd](https://user-images.githubusercontent.com/46839654/69908483-dbaf3d00-142d-11ea-9ef7-6e4fa63b260d.png)
   > >
   > > `"editor.formatOnSave": true` 추가
   >
   > VSC 내에서 터미널을 사용할 수 있는데, `cmd`, `bash(WSL)` 등등 설정해서 사용할 수 있다.
   >
   > > Windows 사용자라면 기본값으로 cmd가 적용되어 있다.
   >
   > 자신이 Windows 사용자이고, VSC의 기본 터미널을 바꾸고 싶다면 아래와 같이 하면 된다.
   >
   > > Microsoft Store에서 `Ubuntu`를 설치한다.
   > >
   > > ![ubuntu](https://user-images.githubusercontent.com/46839654/69894779-fae39700-1367-11ea-9e65-d3e397341e91.png)
   > >
   > > 설치가 끝나면 실행해서 잠시 기다린 다음, username과 password를 입력한다.
   > >
   > > 이건 Ubuntu지만 아무것도 설치되어있지 않기 때문에 [여기](https://docs.microsoft.com/ko-kr/windows/nodejs/setup-on-wsl2)에서 node.js 설정법을 참고해보자.
   > >
   > > Ubuntu에는 기본적으로 Git이 설치되어 있다. (여기에 설치되어 있다 하더라도 vsc 용 윈도우 git도 설치해야 한다)
   > >
   > > Node.js를 설치한 후, git config을 해줘야 한다. `user.name`과 `user.email`을 설정해주자. + 단축 config
   > >
   > > `Ctrl` + `,`으로 VSC 설정을 연다. 그런 다음 `terminal.integrated.shell.windows`을 검색한다.
   > >
   > > cmd를 사용하는 경우 : "terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe"
   > >
   > > WSL을 사용하는 경우 : "terminal.integrated.shell.windows": "C:\\Windows\\System32\\bash.exe"

---