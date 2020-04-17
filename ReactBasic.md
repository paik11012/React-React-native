# React 기본



참고자료: 공식문서 https://ko.reactjs.org/docs/introducing-jsx.html

## 기본적 설치

첫 앱 만들기

새로운 싱글페이지 어플리케이션 만들기(이름 my-app)

```
npx create-react-app my-app
```



## 리액트의 문법 JSX

### Javascript 기반 문법

```react
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### FOR / IF 문 이용

user정보가 있으면 이름을 표시하고 없으면 stranger로 표시하기

```react
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### JSX 속성 정의하기

```react
const element = <div tabIndex="0"></div>;
const element = <img src={user.avatarUrl}></img>;
```

### camelCase 이용하기

### 자식 정의하기

```react
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

 element 안에 긴 html넣기



## DOM에 엘리먼트 렌더링하기

```react
<div id="root"></div>

const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

루트 돔 노드

element를 root dom node에 렌더링하겠다



## 렌더링 된 엘리먼트 업데이트

### 1초마다 바뀌는 시계 만들기

UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 [`ReactDOM.render()`](https://ko.reactjs.org/docs/react-dom.html#render)로 전달하는 것

```react
<div id="root"></div>
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}
setInterval(tick, 1000);
```

tick라는 함수를 만들고 그 안에 element를 만들었다

그곳에서 h2는 date를 보여준다

ReactDOM.render(element, document.getElementById('root')); 이를 root dom에 렌더링한다(보여주기)

함수를 정의한 한 후 1초마다 setInterval 콜백함수를 이용해 ReactDOM.render를 호출한다.



## Components and props

### 컴포넌트

```react
function Welcome(props) {  return <h1>Hello, {props.name}</h1>;}
const element = <Welcome name="Sara" />;ReactDOM.render(
  element,
  document.getElementById('root')
);
```

React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달합니다. 이 객체를 “props”라고 합니다.

### Props

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(element, document.getElementById('root'));
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



## app.js 다뤄보기

제일 먼저 렌더링 되는 곳이 app.js다

```react
import React from 'react';
import { Text, View } from 'react-native';

export default function YourApp() {
  return (
    <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}>
      <Text>
        Try editing me! 🎉
      </Text>
    </View>
  );
}
```

