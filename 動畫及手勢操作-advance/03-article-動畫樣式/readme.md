# 動畫樣式設定

## 使用方式

首先要決定想做的動畫需要的樣式和變量值，在初始化 state 時用 Animated.Value 初始化動畫值 ，並在樣式屬性綁定 state 中的 Animated value 變量值，當動畫執行時，變量值的變化會更新渲染綁定的樣式。

## 動畫值

### 單個動畫值

> 記得使用 new !!!

`Animated.Value()`

```js
new Animated.Value(0)
```

### 動畫向量值

`Animated.ValueXY()`

```js
new Animated.ValueXY({ x: 15, y: 15 })
```

### 初始化範例

```js
state = {
  animValue: new Animated.Value(0),
}
```



##  動畫設定與執行

使用 Animated API 設定動畫類型更新 Animated state 的值，再透過 start function 開始執行動畫。

淡入動畫範例

```js
import React from 'react';
import { Animated, Text, View } from 'react-native';

class FadeInView extends React.Component {
  // 在 state 初始化宣告動畫的樣式值
  state = {
    fadeAnim: new Animated.Value(0),  // 透明度初始值 0
  }

  componentDidMount() {
    // 選擇 timing 動畫函數
    Animated.timing(
      this.state.fadeAnim,            // 動畫的樣式變量值
      {
        toValue: 1,                   // 動畫完成時的變量值
        duration: 10000,              // 動畫過程時間 (ms 毫秒)
      }
    ).start();                        // 開始執行動畫
  }

  render() {
    let { fadeAnim } = this.state;

    return (
      <Animated.View                 // 使用支援動畫的元件
        style={{
          ...this.props.style,
          opacity: fadeAnim,         // 綁定樣式為動畫變量值
        }}
      >
        {this.props.children}
      </Animated.View>
    );
  }
}
```

