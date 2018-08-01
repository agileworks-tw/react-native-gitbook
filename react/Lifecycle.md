# Lifecycle

> 組件的生命週期

![LifeCycle](https://s3.amazonaws.com/media-p.slid.es/uploads/657937/images/3601681/reactjs_component_lifecycle_functions.png)

> #### 練習： [Lifecycle Sample: <https://snack.expo.io/@dmoon/lifecycle-sample>](https://snack.expo.io/@dmoon/lifecycle-sample)

## render

- 每個 React Component 都必需定義的方法，負責繪製 UI 的結構（Virtual DOM 節點結構）
- 必須 return 僅一個 React Element，所以 Component 結構第一層才只能有一個節點

- 每次 Component 成功重繪的生命週期中都會被呼叫到並執行

## componentDidMount

- 在 Component 初始化並且首次繪製完成實際 UI 後觸發，重繪時不會觸發
- 在 Component 的實際 UI 從畫面中移除之前，只會發生一次
- 通常一些首次進入畫面後想發生的事情就適合在這裡呼叫，例如發送 HTTP Request 向後端 API 請求資料

> #### 練習： [DidMount Sample: <https://snack.expo.io/@dmoon/didmount-sample>](https://snack.expo.io/@dmoon/didmount-sample)

## componentDidUpdate

> 不能在沒有條件下進行 setState，否則會無窮迴圈
> 一般會透過新舊比較 ( prevProps 與 this.props ) 或是 ( this.props 與 nextProps )，state 比較亦同
> 再更新 state

```jsx
componentWillUpdate(nextProps, nextState) {

}

componentDidUpdate(prevProps, prevState) {

}
```
