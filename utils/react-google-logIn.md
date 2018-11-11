# React Google Login

> react google login에 대해 공부해보자



```js
import React from 'react';
import ReactDOM from 'react-dom';
import GoogleLogin from 'react-google-login';
// or
import { GoogleLogin } from 'react-google-login';
 
 
const responseGoogle = (response) => {
  console.log(response);
}
 
ReactDOM.render(
  <GoogleLogin
    clientId="658977310896-knrl3gka66fldh83dao2rhgbblmd4un9.apps.googleusercontent.com"
    buttonText="Login"
    onSuccess={responseGoogle}
    onFailure={responseGoogle}
  />,
  document.getElementById('googleButton')
);
```

> clientId는 어떻게 알 수 있지....?



### 성공했을 때, 콜백 (onSuccess callback)

- response타입이 `code`가 아니면, 콜백함수는 GoogleAuth 객체를 리턴한다.
- response타입이 `code` 이면, 콜백함수는 우리 서비스 서버에서 사용할 수 있는 오프라인 토큰을 리턴한다. 
- 호스팅된 도메인 파라미터를 쓴다면, 우리의 백엔드 서버로 구글에서 리턴된 `id_token`*(JSON 웹토큰)*을 검증 해야한다.  
  1. `responseGoogle(response) {...}` 이라는  콜백함수에서,  `response.hg.id_token`에 있는 JWT를 받는다.
  2. 우리의 서버에 이 토큰을 보낸다.(`Authorization` header에 담아서!)
  3. 서버에서 `id_token`를 디코드하는 common JWT 라이브러리 (*ex) jwt-simple*) 를 사용하거나 또는 `https://www.googleapis.com/oauth2/v3/tokeninfo?id_token=YOUR_TOKEN_HERE`여기에 get 요청을 보낸다.
  4. 리턴된 디코드 토큰은 당신이 정한 호스팅된 도메인과 같은`hd`키를 가지고 있어야 한다. 



### 로그아웃

> 구글로그아웃 버튼을 사용하여 로그아웃할 수 있다.

```js
import { GoogleLogout } from 'react-google-login';
    <GoogleLogout
      buttonText="Logout"
      onLogoutSuccess={logout}
    >
    </GoogleLogout>
```












