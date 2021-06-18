# [Messenger App] 채팅 프로그램 만들기 #1



##  *TEMPLATE*

Bootstrap 을 뒤적이다 마음에 드는 디자인 테마 발견!! [메신저 템플릿][https://themes.getbootstrap.com/product/messenger-responsive-bootstrap-application/] 개인적으로 맘에 드는 디자인에 꽂혀서 템플릿에 필요한 기능들을 만들어 보고자함. 마침 채팅 앱 구현에도 관심이 있어서 나이스~



![ㅇㅁㅇㄹ](https://themes.getbootstrap.com/wp-content/uploads/2020/01/Messenger-Responsive-Bootstrap-Application2-1200x900.jpg)



기본적인 로그인/로그아웃, 회원가입 기능들과 채팅방 개설및 멤버관리나 친구등록등의 기능들을 구현하기 위해

**```SpringBoot```** 를 사용해서 rest api 서버를 구현할 계획이고, DB 조회는 **```Spring JPA```**를 이용

인증,권한 관리를 위한 **```Spring Security```**, 를 사용하여 채팅기능을 구현하기 위해 **```WebSocket, Stomp```**, 화면단은 **```Vue Framework```** 로 구현하였다.  <!--(사실 토이프로젝트 정도로 생각했는데.. 하다보니 일이 너무커져서 죽겠.. )-->



## 템플릿 구조

화면단 기술들이 너무 빨리 변하고 있어서 빌드툴을 사용한 템플릿을 처음봄.

그래서 구조부터 살펴보기로 함.

구매한 템플릿은 [gulp][https://gulpjs.com/] 를 사용하여 빌드되어 있었음.

<img src="/Users/lee.yb/Documents/workspace/Blog/lee-yb.github.io/assets/images/gulp_dir_str.png" alt="디렉토리구조" style="zoom:50%; float:left" />

```npm install gulp-cli -g``` gulp를 콘솔에서 사용할 수있게 하는 유틸리티 도구인 gulp-cli를 글로벌 영역에 설치.

```npm install``` 로 의존성 모듈들을 설치하고

```gulp``` 명령어를 통해 gulpfile.js 실행.

자세한 내용은 나중에 webpack 공부할때 정리를 하고 

