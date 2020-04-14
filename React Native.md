# React Native

환경설정

```
choco
node
python
java
javac
npm install -g react-native-cli
react-native --version
android studio
```

프로젝트 시작

```
react-native init FirstApp
npx create-react-app my-app
```



## 컴포넌트

컴포넌트 활용해 React에게 화면에 표현하고 싶은 것이 무엇인지 알려주기

데이터가 변경될 때 React는 컴포넌트를 효율적으로 업데이트하고 다시 렌더링

ShoppingList는 **React 컴포넌트 클래스** 또는 **React 컴포넌트 타입**

개별 컴포넌트는 `props`라는 매개변수를 받아오고 `render` 함수를 통해 표시할 뷰 계층 구조를 반환

[ RENDER 함수 ]

`render` 함수는 화면에서 보고자 하는 *내용*을 반환, React는 설명을 전달받고 결과를 표시. 특히 `render`는 렌더링할 내용을 경량화한 **React 엘리먼트**를 반환(JSX문법)

```react
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// 사용 예제: <ShoppingList name="Mark" />
```



## TIC TAC TOE

```
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
```

board의 value를 square에 전달하기

```
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

클릭하면 alert 뜨도록

```
<button className="square" onClick={function() { alert('click'); }}>
  {this.props.value}
</button>
```

`onClick={() => alert('click')}`이 어떻게 동작하는지 살펴보면 `onClick` prop으로 *함수*를 전달하고 있습니다. React는 클릭했을 때에만 이 함수를 호출할 것입니다.



### X표시 채우기 = STATE 이용하기(생성자 추가)

```
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }
```

React 컴포넌트는 생성자에 `this.state`를 설정하는 것으로 state를 가질 수 있습니다. 이제 Square의 현재 값을 `this.state`에 저장하고 Square를 클릭하는 경우 변경하겠습니다.

(React 컴포넌트 클래스는 `생성자`를 가질 때 `super(props)` 호출 구문부터 작성)

```
  render() {
    return (
      <button 
      className="square" 
      onClick={() => this.setState({value: 'X'})}>
        {this.state.value}
      </button>
    );
  }
```

클릭하면 state를 X로 바꾸고 그 버튼 자리에 state인 X를 표시한다.



## STATE 한 곳에서 관리하기

여러개의 자식으로부터 데이터를 모으거나 두 개의 자식 컴포넌트들이 서로 통신하게 하려면 부모 컴포넌트에 공유 state를 정의해야 합니다. 부모 컴포넌트는 props를 사용하여 자식 컴포넌트에 state를 다시 전달할 수 있습니다. 이것은 자식 컴포넌트들이 서로 또는 부모 컴포넌트와 동기화 하도록 만듭니다.

```
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }
  renderSquare(i) {
    return <Square value={this.state.squares[i]} />;
  }
```

상위 컴포넌트인 board에 props를 정의한다, 그 state에 9개의 array를 만들고 null로 채운다

사각형에 표시되는 것도 

```
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }
  renderSquare(i) {
    return <Square value={this.state.squares[i]}
    onClick={() => this.handlecClick(i)} />;
  }
```

아래 rendersquare코드 수정하기

Square가 Board를 변경할 방법이 필요(하위 컴포넌트가 상위 컴포넌트 바꾸기)



