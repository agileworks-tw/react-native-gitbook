# 在 RN 專案中使用

現在我們已經成功連結兩個專案，接下來我們需要在 React Native 專案中使用已經完成的 native module。

## Import module

首先，我們必須要 import 已經 link 好的 module。請切換到本教學一開始就建立好的 React Native 專案目錄，找到 `App.js`。

請在最上方加入以下程式碼：

```javascript
import MyAndroidToast from 'react-native-my-android-toast';
```

現在起即可在需要的地方，透過以下方式呼叫 Toast！

```javascript
// 輸出 'hi! My Project is TOSTED!' 文字，
// 並指定顯示時間為 MyAndroidToast.SHORT
MyAndroidToast.show('My Project is TOSTED!', MyAndroidToast.SHORT);
```

## 完整程式碼

在以下範例中，我會加入一個 React Native Button 元件，並透過它執行 Toast。

```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

import React, { Component } from 'react';
import {
  // 加入 Button
  Button,
  Platform,
  StyleSheet,
  Text,
  View
} from 'react-native';
// 引入製作好的 Native module `MyAndroidToast`
import MyAndroidToast from 'react-native-my-android-toast';

const instructions = Platform.select({
  ios: 'Press Cmd+R to reload,\n' +
    'Cmd+D or shake for dev menu',
  android: 'Double tap R on your keyboard to reload,\n' +
    'Shake or press menu button for dev menu',
});

export default class App extends Component<{}> {
  
  showToast = () => {
		// 印出預先定義的 MyAndroidToast.SHORT 常數
    console.log('MyAndroidToast.SHORT=>', MyAndroidToast.SHORT);
		// 印出  MyAndroidToast 內容方便觀察
    console.log('MyAndroidToast=>', MyAndroidToast);
		// 操作 MyAndroidToast 呼叫 Android Toast
    MyAndroidToast.show('My Project is TOSTED!', MyAndroidToast.SHORT);
  }

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit App.js
        </Text>
        <Text style={styles.instructions}>
          {instructions}
        </Text>
				
        <Button onPress={this.showToast} title="TOAST ME!"></Button>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

```
