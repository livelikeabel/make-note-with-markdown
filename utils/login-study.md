# Login study

많은 로그인 방법들이 있다.



인증(Authentication)

권한부여(Authorization) : 리소스에 대한 권한부여



### OAuth란?

- 인증과 권한부여의 여러 방법중 하나이다.
- 서버와 클라 사이의 인증을 완료할시, 권한부여의 결과로 서버가 `access token`을 준다.
- 클라이언트는 `access token`을 이용해서 접근 및 서비스 요청 가능.
- 서버는 `access token`을 통해 권한을 확인하여 접근 여부를 결정하고 결과 데이터를 클라이언트에 보내준다.
- `access token`을 사용하기 때문에, `session`이나 `cookie`로 상태정보를 유지할 필요가 없다.

- 외부서비스(3-party app)의 인증 및 권한부여를 관리하는 범용 프레임 워크이다. 
- OAuth 기반 서비스의 API를 호출 할 때는, <u>HTTP헤더에 access token을 포함해서 요청</u>을 보낸다.



### OAuth를 구성하고 있는 주요 4가지 객체(Roles)

- `resource owner`(자원 소유자)는 `protected resource`(보호된 자원)에 접근하는 권한을 제공한다.
- `resource server`(자원 서버)는 **acess token**을 사용해서 요청(request)을 수신할 때, 권한을 검증한 후 적절한 결과를 응답한다.
- `client`는 `resource owner`의 `protected resource`에 접근을 요청하는 애플리케이션이다.
- `authorization server`(권한 서버)는 `client`가 성공적으로 **access token**을 발급받은 이후에 `resource owner`(자원 소유자)를 인증하고 `obtaining authorization`(권한부여)를 한다. 

> Q. authorization server가 누구지? 예를 들면 google...?



예를 들면, 

1. 나의 `client app`에서 clientId와 함께 google에 요청을 보낸다.
2. google 계정으로 로그인을 한다.
3. (로그인 성공시) response로 `access token`을 받는다
4. access token을 통하여 api서버에 자원을 요청할 수 있게 된다.



#### Access Token

- 요청 절차를 정상적으로 종료한 클라이언트에게 발급된다.
- 보호된 자원에 접근할 때 권한 확인용으로 사용된다.
- 문자열 형태
- 클라이언트에 발급된 권한을 대표한다.
- 리소스 서버는 이 토큰 하나로 권한을 확인할 수 있다.



#### Refresh Token

- `access token`의 유효기간이 만료되면, 새로운 `access token`을 얻어야 하는데, 그 때 사용된다.
- `access token`이 발급될 때, `refresh token`도 함께 발급된다. 그래서 미리 `refresh token`을 가지고 있을 수 있다.
- 클라이언트가 오류 등으로 `access token`이 만료됨을 알면, 가지고 있던 `refresh token`을 권한 서버에 보내어 새로운 `access token`을 요청한다.







> ### 질문
>
> - 클라의 react-google-login을 jwt관련해서 쓰고 있는거 같은데
> - - 백엔드는 passport, session, oauth...? 써도 되나…?(사실 뭔 차이인지도 모르겠다...)
>   - 아니면 백엔드에서도 jwt를 써야하나...?
>
> - jwt의 response로 받는 토큰?은 어디에 넣어야 하나? localstorage에 넣어도 되는가...?
> - google login을 해서, 클라가 access token 을 가지고 있다면, 어디에 저장해두고 써야할까....?
> - access token은 누가 발급하는가? 구글에서? 우리 서버에서?
>   - 구글에서 발급해주는듯!
>   - 근데 refresh token은 안주는데...?
>   - tokenId 와 tokenObj와 googleId를 주고 있는데, 그 중에 하나가 refresh token과 비슷한 역할을 하지 않을까...?







> 출처 :
>
> - OAuth 관련
>
>   - 인증과 권한부여의 필요성 : http://blog.weirdx.io/post/39955
>