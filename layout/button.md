# React Native 按鈕元件

## Button

- 0.38 版才開始支援
- 只支援最低限度的客製化
  - title
  - color
  - onPress
- iOS、Android 樣式不一樣

![Button Example](https://facebook.github.io/react-native/docs/assets/buttonExample.png)

使用範例:

```jsx
<Button
  onPress={() => {}}
  title="Hello"
  color="#841584"
/>
```

Button 範例：[https://snack.expo.io/@dmoon/button-example](https://snack.expo.io/@dmoon/button-example)

## Touchable 元件

- TouchableHighlight
  - 點擊後反黑
- TouchableNativeFeedback
  - Android 會有 Material 效果
- TouchableOpacity
  - 點擊後變透明

點擊範圍

```js
hitSlop = {
  top: 0,
  left: 100,
  bottom: 0,
  right: 100
}
```

### TouchableOpacity

是最常用的按鈕元件，含有 onPress prop 的可按視圖元件(View)，可以用來包裝想要加上按扭事件的組件

props

- onPress

```jsx
<TouchableOpacity onPress={this._onPressButton}>
  <Image
    style={styles.button}
    source={require('./myButton.png')}
  />
</TouchableOpacity>
```

客製化按鈕範例:[https://snack.expo.io/@dmoon/custom-button](https://snack.expo.io/@dmoon/custom-button)
