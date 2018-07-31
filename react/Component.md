# Component

- 用來產生 React Element 實體 ( Virtual DOM 節點 )

- 使用 JS 編寫，Component 本身足以完整表達其可能的顯示變化和行為

- 可以自由嵌套或組合，讓前端 UI 程式有更好的可組合性與可重用性

- 自定義封裝資料接口及功能接口

- Component Class 名稱首字母必須大寫 ( 大駝峰式 Upper Camel Case )

- 在元件的 render 方法中，return React Element 來呈現 UI 內容

- 每個 Component ，render 中只能有一個根節點元素

```jsx
import React, { Component } from 'react';
import { Text, View } from 'react-native';

class App extends Component {
  render() {
    return (
      <View>
        <Text>Welcome to React Native!</Text>
      </View>
    );
  }
}
```

## Component 重用組合

```jsx
// Greeting Component
class Greeting extends Component {
  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}
```

```jsx
// LotsOfGreetings Component
class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{ alignItems: 'center' }}>
        <Greeting name="React" />
        <Greeting name="Native" />
        <Greeting name="JavaScript" />
      </View>
    );
  }
}
```

![Component Composition Demo](https://s3.amazonaws.com/media-p.slid.es/uploads/40413/images/4595448/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2018-02-10_%E4%B8%8A%E5%8D%886.04.35.png)
