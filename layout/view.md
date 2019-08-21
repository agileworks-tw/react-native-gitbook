# View 樣式

- 支援 [Flexbox](https://facebook.github.io/react-native/docs/flexbox.html) 佈局
-[Style](https://facebook.github.io/react-native/docs/style.html)

常用 style:

```text
backgroundColor: 背景顏色
flex: 排版方式
weight: 寬度
margin: 邊界
padding: 留白、內距
borderRadius: 圓弧
borderColor: 邊框顏色
borderWidth: 邊框寬度
```

特殊 props:

```text
elevation 使用 Android 原生的 elevation API 來設置 View 的高度產生陰影的效果
```

```js
import React, { Component } from 'react';
import {
  View,
} from 'react-native';

export default class ViewSample extends Component {
  render() {
    return (
      <View style={{ flex: 1 }}>
       <View style={{backgroundColor: 'red', flex: 1}} />
       <View style={{backgroundColor: 'blue', flex: 1}} />
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center', }}>
          <View elevation={10} style={{ height: 100, width: 100, backgroundColor: '#eee', justifyContent: 'center' alignItems: 'center' }}>
            <Text>123</Text>
          </View>
        </View>
      </View>
    );
  }
}
```

## ScrollView

ScrollView 是可以捲動的視圖元件，在內容高度高於裝置高度時，提供捲動功能。

```jsx
<ScrollView>
  {/* content */}
</ScrollView>
```

使用範例: [https://snack.expo.io/@dmoon/scrollview-sample](https://snack.expo.io/@dmoon/scrollview-sample)