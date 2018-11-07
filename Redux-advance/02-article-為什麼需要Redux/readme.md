# 為什麼需要 Redux ?

Redux 作者 Dan Abramov：

> "如果你不知道是否需要 Redux，那就是不需要它。"

你可能不需要 Redux：[https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)

單頁面應用漸趨複雜，我們需要處理頁面上許多不同資料來源的資料操作同步問題

**jQuery 資料操作同步範例**

範例連結： [http://jsfiddle.net/dmoon/87sakwed/1](http://jsfiddle.net/dmoon/87sakwed/1)

**React 資料操作同步範例**

- React component 的 state 彼此獨立
- 透過 props 傳遞的 callback func ，才能修改父 component 的 state

範例連結： [http://jsfiddle.net/dmoon/22x2a7sq/26](http://jsfiddle.net/dmoon/22x2a7sq/26)

## 結論：使用情境

React 應用開發過程中最常遇到的需要情境:
`需要在 Component 間共享、維護某些狀態資訊`，像是與伺服器交互複雜、 畫面需要管理多個資料來源的應用情況

Component 之間的狀態管理空間為 state，但每個 component 的 state 都是獨立的，與其他 component 間只能透過 prop 進行資訊傳遞，因此若要保持 Single Source of Truth 的特性，必須要將狀態資料儲存在共同的父層管理，再經由 prop 一路往下傳遞， 這樣的作法會造成相當複雜的耦合性

**使用場景：**

- 共享某個组件的狀態
- 需要改變別的組件的狀態
- 共用某個全域狀態，讓所有組件都能取得