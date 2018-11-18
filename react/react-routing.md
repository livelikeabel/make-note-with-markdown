# React Routing

SPA는 단일 페이지 애플이케이션 이기에 URL변경이 되는 일이 없다.(브라우저 렌더링 덕분에 서버에 연결할 이유가 없다.)

그로 인해 몇가지 문제들이 생긴다.

- 브라우저를 <u>새로고침 하면</u> 읽고 있던 페이지의 원래 폼으로 돌아간다.
- 브라우저의 기록 기능은 접속해 있던 사이트의 단일 URL만 기록하므로 브라우저의 뒤로가기 버튼을 눌렀을 때 완전히 다른 사이트로 이동할 수 있다. <u>페이지의 내용은 변경하면서 URL은 변경되지 않았기 때문이다.</u>
- 친구들에게 사이트의 특정 페이지를 공유할 수 없다.
- 첫 페이지와 URL을 구분할 수 없으므로 검색 엔진이 사이트를 색인할 수 없다.



=> **URL 라우팅**을 하여 이런 문제를 방지할 수 있다.(*SEO: Search Engine Optimization* 에도 도움된다.)

> - URL 라우팅은 사용자 친화적이며 잘 설계된 웹 앱의 요구사항이다. (링크저장, 공유시 app의 상태보존을 위함)



## React Router

1. URL에 대응하는 웹 페이지의 마크업이 될 React 컴포넌트에 대한 맵핑을 생성한다.
2. React Router의 Router 컴포넌트와 Route 컴포넌트를 이용하면 URI의 변경에 따라 화면을 마술처럼 변경할 수 있다.
3. `ReactDOM.render()`를 사용해서 일반적인 React 엘리먼트처럼 웹 페이지에 라우터를 렌더링한다.



### Route

- 각 Route는 최소 두 가지 속성(props)을 갖는다.

  1. path: 이 경로에 적용되는 URL 패턴

  2. component: 필요한 컴포넌트를 가져와서 렌더링하기 위한 props 

  > Route에 이벤트 핸들러나 데이터 같은 다른 속성을 추가할 수도 있다. (`props.route`로 접근할 수 있다.)

- Route 컴포넌트를 중첩하여 부모의 레이아웃을 재사용할 수 있다.

- 중첩과 무관하게 독립적인 URL을 적용할 수 있다.



### withRouter 고차 컴포넌트를 이용해서 라우터에 접근하기

컴포넌트 인자로 받아 router에 주입하고 다른 고차 컴포넌트를 반환한다.

> 예를 들어, 아래와 같이 `Contact`에 router를 주입할 수 있다.
>
> - 상태비저장 컴포넌트에도 사용할 수 있다!

```js
const { withRouter } = require('react-router')
...
<Router ...>
    ...
	<Route path="/contact" component={withRouter(Contact)} />
</Router>
```

