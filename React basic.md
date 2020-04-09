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



## 변경된 부분만 업데이트 하기



