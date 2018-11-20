# Child Element rendering

> 자식 컴포넌트를 얼마든지 추가할 수 있는 범용 컴포넌트를 만들기

**children** 속성

- 모든 자식을 `{this.props.children}`으로 렌더링할 수 있는 간편한 방법이다.
- 자식 엘리먼트가 하나 이상 있는 경우에 배열이 된다.
   - ```{this.props.children[0]}``` 이런식으로 접근 가능하다.
- 자식을 다룰 때 사용할 수 있는 헬퍼 메서드
   - React.Children.count()  :  자식 엘리먼트 수를 셀 때.
   - React.Children.map()
   - React.Children.forEach()
   - React.Children.toArray()

