# 常用組件教學

## 組件使用方式

首先可以到官方文件: [https://facebook.github.io/react-native/docs/getting-started](https://facebook.github.io/react-native/docs/getting-started)

點上方的 `API` Tab 後，可以在左側的 Components 列表中找到各組件提供的 props 、methods 與使用方式，許多組件也有提供 Expo Snack 的線上範例。

我們先從最基本的 `View` UI 組件開始吧。

## View

View Docs: [https://facebook.github.io/react-native/docs/view](https://facebook.github.io/react-native/docs/view)

View 是 React Native 中建構 UI 的基礎元件，支援 [Flexbox](https://facebook.github.io/react-native/docs/flexbox.html) 佈局、[Style](https://facebook.github.io/react-native/docs/style.html)、一些觸摸處理、和一些無障礙功能的容器，並且它可以放到其它的視圖裡，也可以有任意多個任意類型的子視圖。不論在什麼平台上，View 都會直接對應一個平台的原生視圖，無論它是 UIView、div 還是 android.view 等等

```jsx
class ViewColoredBoxesWithText extends Component {
  render() {
    return (
      <View
        style={{
          flexDirection: 'row',
          height: 100,
          padding: 20,
        }}>
        <View style={{backgroundColor: 'blue', flex: 0.3}} />
        <View style={{backgroundColor: 'red', flex: 0.5}} />
        <Text>Hello World!</Text>
      </View>
    );
  }
}
```

線上範例：[https://snack.expo.io/@dmoon/official-view-sample](https://snack.expo.io/@dmoon/official-view-sample)