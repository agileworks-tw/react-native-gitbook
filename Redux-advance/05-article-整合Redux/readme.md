## React Redux 運作方式

將 react-redux 的 Provider Component 作為 React 專案的 Root Component，這樣 Provider 就會是所有 children component 的共同父元件，之後透過 Connect 方法將 Component 與 Redux 連接，Provider 便可以透過 prop 將 component 需要的資料一路往下傳遞到透過 connect 方法連接 Redux 的 component

![](assets/2018-10-15-11-43-12.png)

## Smart Component / Dumb Component

|                    | 容器組件 (Smart Component) | 展示組件 (Dumb Component) |
| ------------------ | -------------------------- | ------------------------- |
| **位置**           | 最頂層，路由處理           | 中間和子組件              |
| **連結 Redux**　　 | 是                         | 否                        |
| **讀取數據**       | 從 Redux 獲取 state        | 從 props 獲取數據         |
| **修改數據**       | 向 Redux 派發 actions      | 從 props 調用回調函數     |