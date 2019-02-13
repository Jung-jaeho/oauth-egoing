###oauth



   - oauth 란?
  

  1.https://developers.google.com/identity/protocols/OAuth2

  2.html + javascript 이용   -> client 측 애플리케이션

    Google API 콘솔에서 OAuth 2.0 자격증을 얻으십시오.
      OAuth 2.0 자격증필요

    Google 인증 서버에서 액세스 토큰을 얻습니다.
    API에 액세스 토큰을 보냅니다.



    우리가 하는 건 클라이언트 측 (JavaScript) 애플리케이션
    
    consent -> 페이스북에 접속을 허가하시겠습니까?


    a(user)   b(it-pro) c(google)

    c에 id와 비밀번호 (구글의 사용자의 아이디와 비밀번호)

    a->b 에게 id/pwd 기록


oauth는 어떻게 동작하는가

a 사용자의 자원(resource oner) = 페이스북 뉴스피드, 구글 캘린더 올릴 사람 
b 그들의 서비스 ( resource server) = 구글,페이스북
c 사용자(client)  = it-pro 홈페이지

1. 우리의 서비스가 구글서비스를 사용하려면 승인을 받아야 한다.
    (구글 서비스에 가서 승인을 받는다.->승인이 떨어지면 사업자번호와 같은 번호를 준다,, ==국세청 사업자 승인
    -> 사업자 등록번호를 준다, == 본인이 태어난 출생신고를 해면 주민번호를 준다.)


구글이 -> client 에게 
client_id = a;  (다른사람 봐도됨)
client_secret : b;(절대 노출 X)

이렇게 받고 우리는 2가지를 다 받았다.


이상태에서 b 가 c한테 이 일을 하려면 리소스 서버에 대해서
구글의 캘린더 기능을ㄹ 승인하셔야 합니다 라고 뜬다. 

그러면

b는 a에 접속을 해서 화면에 it-pro가 당신의 google 캘린더에
접근하려고 하는데 허락할껍니까?
(ex 페이스북 게시권한을 요청)


access_token을 받급받는것이 제일 중요하다.

아무튼 그래서 access_token값을 만들고 

access_token : c (한시간 또는 한달동안만 사용할수있다. 하지만 아무런 정보는 없고 아이디와 패스워드를 제외하고 그런것이다)
user:ego
scope: canlendar(많은 서비스중 캘린더만 승인한다.)


가 구글에서 생긴다.


그럼 구글은 리소스 오너를 통해서 클라이언트로 access token : c를 알게된다.(클라이언트는 사용자의 개입없이 client로 돌아온다.)


access_token을 통해서 인증을 받게되면 다양한플랫폼을 동작할수 있다.구글에있는 특정기간 특정시간동안 사용할수 있다.




시작.. 첫번째 단계

1. Google API(등록하는 창구) 콘솔에서 OAuth 2.0 자격증(사전동의)을 얻으십시오.(사업자등록)

2. Google 인증 서버에서 액세스 토큰(사용자에 대한 임시비밀번호)을 얻습니다.


3. API에 액세스 토큰을 보냅니다.(구글 캘린더를 보고싶어요 access token 권한을 보고 캘린더 써 )

4. 필요한 경우 액세스 토큰을 새로 고칩니다.(짧게 1시간 길게 60일) ->자동화 refresh token


다시사진

기능을 쓰려고하면 로그인을 하고 동의화면을 보여준다.(content)

사용자가 허락하면 access token을 응답한다. 
==
<------- token respeonse


그다음 서버에 요청하면 된다.



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
클라이언트 측 웹 애플리케이션 용 OAuth 2.0
https://developers.google.com/identity/protocols/OAuth2UserAgent

프로젝트 하나는 서비스 하나이다.

itpro-oauth

프로젝트 만들고

사용자 인증정보 클릭

사용자 인증정보 만들기 클릭->oauth 클라이언트 id


OAuth 클라이언트 ID를 만들려면 먼저 동의 화면에서 제품 이름을 설정해야 합니다.

사용자한테 당신은 어떤서비스 인증을 받으려고 합니까?
-> 동의화면 클릭

애플리케이션 이름 = social_login

이름 : web app 1

승인된 자바스크립트 원본 = 당신은 이도메인에서만 사용할수있어요
(당신 여기서만 장사해야 합니다.)

http://localhost:8080

->생성 -> 확인(클라이언트id, 클라이언트 secret 생성)

빨강색 글씨까지 완성

클라이언트에서 구글로갔다가 구글에서 다시 클라이언트로 온것

여기까지는 나이제 구글에 등록할꺼야 까지했음


Web Server for Chrome 설치


http://localhost:8080/




widget sdk raw


https://developers.google.com/identity/sign-in/web/sign-in


구글 버튼을 만드는 코드

https://developers.google.com/identity/sign-in/web/


구글 캘린더 

https://developers.google.com/calendar/




https://developers.google.com/calendar/v3/reference/calendarList/list




스코프(읽기만 하겠다) -> https://www.googleapis.com/auth/calendar.readonly

추가

클라이언트 아이디 추가

<meta name="google-signin-client_id" content="663913350605-c5ad5hdq03o2a8gtk1ba4d5veg25kqcb.apps.googleusercontent.com ">



로그인버튼 추가 
<div class="g-signin2"></div>



집가서 설명해봐라

오늘 강의는 access 토큰을 획득하는것이 목표다.





























