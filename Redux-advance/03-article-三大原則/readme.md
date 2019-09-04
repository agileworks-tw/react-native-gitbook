# 三大原則

## Single source of truth 　(單一資料來源)

整個應用的 state 存在一棵 object tree 中，並且放在唯一的 container (store) 內

## State is read-only

唯一改變 state 的方法就是觸發 action (修改資料的申請動作)

## Changes are made with pure functions

對應不同的 action，使用純函數編寫 reducer 來執行 state 修改

