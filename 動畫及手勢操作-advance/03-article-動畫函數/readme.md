# 動畫函數

React Native 提供下列三種動畫函數類型，分別有著不同的函數曲線，影響動畫從初始值到最終值的過程。

- `timing`：使用 easing 函数隨著時間更新動畫數值
  - easing: [https://facebook.github.io/react-native/docs/easing#docsNav](https://facebook.github.io/react-native/docs/easing#docsNav)
- `decay`：以指定的初始速度開始動畫，並且設定一個衰弱值，逐漸緩慢停下 
- `spring`： 提供一個簡單的彈簧  物理模型 

##  執行/停止動畫

調用動畫函數的 start 函數來開始動畫，start 函數可以傳入一個 callback 函數，在動畫完成時調用。

```js
Animated.timing(
  this.state.fadeAnim, // 動畫的樣式變量值
  {
    toValue: 1, // 動畫完成時的變量值
    duration: 10000 // 動畫過程時間 (ms 毫秒)
  }
).start();
```

一般動畫大多使用 `timing` 函數  來配置，不同的動畫函數有各自的配置參數，詳細可以參考文件，這邊以 `timing` 為例介紹

## timing 函數參數

timing(value, config)

- duration: 動畫持續時間（毫秒），預設值 500。
- easing: 緩動函數，預設為 Easing.inOut。
  - Easing 參數文件: [https://reactnative.cn/docs/easing/](https://reactnative.cn/docs/easing/)
- delay:  開始之前的延遲時間（毫秒），預設為 0。
- useNativeDriver:  是否啟用原生動畫。預設 false。
