# Virtual DOM

> Virtual DOM 是一份純資料的樹狀物件結構，映射對應到實際的 DOM

- 透過 Component ( React.createElement 函數 ) 來產生 Virtual DOM 節點（React Element）
- Virtual DOM 為 Component 提供了中介的虛擬層，讓開發者能以聲明式的方式定義 UI 的顯示邏輯與行為

- 我們透過定義 Component 來表達「UI 什麼情況時該呈現什麼結果」，而不是「UI 什麼情況時該如何改變」 -  差別在有無手動更新的過程

- React 會根據 Virtual DOM 自動幫你完成 UI 畫面的呈現與變化 （ Renderer 的工作）
