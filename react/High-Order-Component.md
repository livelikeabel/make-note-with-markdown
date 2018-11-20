# HOC: high-order component

> 컴포넌트에 추가적인 로직을 적용해서 컴포넌트를 향상시킬 수 있다. 

고차 컴포넌트를 통해 다른 컴포넌트가 기능을 상속받는 패턴이다. 

=> **고차 컴포넌트를 통해 코드 재사용이 가능하다.** *(DIY도 지킬 수 있다.)*

> *결국 중복을 제거하기 위한, 또 하나의 엄청난 방법! 중복을 줄이는건 언제나 즐겁고 멋지고 신나는 일이다!*



<br/>



### 고차컴포넌트 만드는 법

1. **중복**을 찾는다. 

2. 중복되는 기능을 모아서 고차 컴포넌트 함수를 만든다.

   - 고차컴포넌트 함수는 <u>컴포넌트를 인자로 받아서, 컴포넌트를 반환하는 함수</u>다.
   - ex) Tooltip 고차컴포넌트 함수

   ```js
   const Tooltip = Component => {
     class _Tooltip extends React.Component {
       constructor(props) {
         super(props)
         this.state = { opacity: false }
         this.state.handleClick = this.handleClick.bind(this)
       }
   
       handleClick() {
         alert('click the tooltip!')
       }
   
       render() {
         return (
           <Component
             {...this.state}
             {...this.props}
           />
         )
       }
     }
     return _Tooltip
   }
   
   export default Tooltip
   ```

   > Tooltip 고차컴포넌트 함수의 속성을 인자로 들어오는 Component의 속성으로 주입한다.
   >
   > 번외)
   >
   > - handleClick 메서드를 `this.state`에 추가해주고 있다. 어색하다고 생각했는데, state는 컴포넌트 내부의 변수(또는 함수)를 다룬다고 생각하니 괜찮은것 같다. 위의 코드는 Tooltip의 state를 props로 넘겨주고 있다.





***고차 컴포넌트는 훌륭한 코드 추상화 방법이다. 고차 컴포넌트 패턴을 이용하면 재사용 가능한 React 컴포넌트를 작은 모듈로 만들 수있다.*** 



<br/>



### 참고

**펼침 연산자(spread operator))를 사용해서 모든 속성 전달하기**

- 펼침 연산자를 이용하면 객체(obj)의 모든 props를 엘리먼트의 props로 전달할 수 있다.

  `<Component {...obj}>`

- 고차 컴포넌트를 만들 때, 펼침 연산자가 필요했던 이유는 <u>함수에서 인자로 사용할 속성을 미리알 수 없었기 때문</u>이다.

  => 펼침 연산자는 객체 또는 변수의 모든 데이터를 전달하는 <u>포괄문</u>이다.

- 기존의 키, 밸류 선언도 함께 사용할 수 도 있다.

  `<Component {...this.state} {...this.props} className="main">` 

  > 현재 클래스의 모든 상태와 속성, className을 새로운 컴포넌트에 적용하고 있는 경우이다.