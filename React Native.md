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





# 문법

## View란?

a **view** is the basic building block of UI = 모든 것 하나 하나가 뷰로 이루어져 있다



## Core Components

```react
import React from 'react';
import { View, Text, Image, ScrollView, TextInput } from 'react-native';

export default function App() {
  return (
    <ScrollView>
      <Text>Some text</Text>
      <View>
        <Text>Some more text</Text>
        <Image source="https://reactnative.dev/docs/assets/p_cat2.png" style={{width: 200, height: 200}}/>
      </View>
      <TextInput
        style={{
          height: 40,
          borderColor: 'gray',
          borderWidth: 1
        }}
        defaultValue="You can type here"
      />
    </ScrollView>
  );
}
```

주로 쓰이는 건 view, text, image, scrollview, textinput이 있다



## Component 만들기

```react
import React from 'react';
import { Text } from 'react-native';

export default function Cat() {
  return (
    <Text>Hello, I am your cat!</Text>
  );
}

```

리액트와 텍스트를 import한 후 cat이라는 함수를 정의한다.

Whatever a function component returns is rendered as a **React element.**

### JSX 이용 가능

```jsx
import React from 'react';
import { Text } from 'react-native';

export default function Cat() {
  const name = "Maru";
  return (
    <Text>Hello, I am {name}!</Text>
  );
}
```



## Props 이용하기

```react
import React from 'react';
import { Text, View } from 'react-native';

function Cat(props) {
  return (
    <View>
      <Text>Hello, I am {props.name}!</Text>
    </View>
  );
}

export default function Cafe() {
  return (
    <View>
      <Cat name="Maru" />
      <Cat name="Jellylorum" />
      <Cat name="Spot" />
    </View>
  );
}
```

 Props let you customize React components.

cat이라는 함수 안에 props를 넣을 것이라 설정. text안에 props로 온 것들의 name을 넣는다.



## State

**state** is like a component’s personal data storage. State is useful for handling data that changes over time or that comes from user interaction.

배고픈 고양이 먹이주기

```react
import React, { useState } from "react";
import { Button, Text, View } from "react-native";

function Cat(props) {
  const [isHungry, setIsHungry] = useState(true);

  return (
    <View>
      <Text>
        I am {props.name}, and I am {isHungry ? "hungry" : "full"}!
      </Text>
      <Button
        onPress={() => {
          setIsHungry(false);
        }}
        disabled={!isHungry}
        title={isHungry ? "Pour me some milk, please!" : "Thank you!"}
      />
    </View>
  );
}

export default function Cafe() {
  return (
    <>
      <Cat name="Munkustrap" />
      <Cat name="Spot" />
    </>
  );
}
```

useState가 하는 일

### 무언가를 바꾸려고 하면 set이 꼭 필요하다!

- it creates a “state variable” with an initial value—in this case the state variable is `isHungry` and its initial value is `true`
- it creates a function to set that state variable’s value—`setIsHungry`

isHungry랑 setIsHungry 둘 다 true 상태로 시작

버튼 누루면 isHungry가 false로 바뀌고 상태와 title 모두가 바뀐다.

즉 버튼을 누르면 when a state-setting function like `setIsHungry` is called, its component will re-render. 



## Text Input

```react
import React, { Component, useState } from 'react';
import { Text, TextInput, View } from 'react-native';

export default function PizzaTranslator() {
  const [text, setText] = useState('');
  return (
    <View style={{padding: 10}}>
      <TextInput
        style={{height: 40}}
        placeholder="Type here to translate!"
        onChangeText={text => setText(text)}
        defaultValue={text}
      />
      <Text style={{padding: 10, fontSize: 42}}>
        {text.split(' ').map((word) => word && '🍕').join(' ')}
      </Text>
    </View>
  );
}
```

text를 쓰면 onChangeText가 call되어 text를 업데이트 한다

입력된 text를 단어단위로 인식해 단어 하나 당 피자 하나로 번역하고 ` `띄어쓰기 하나로 join한다.



