# ToDo List 練習整合 Redux

難度： 進階

目標： 在 React Native 透過 fetch 使用呼叫後端 API，並透過 Redux 管理狀態

專案： [https://github.com/agileworks-tw/RN_Todo_Sample](https://github.com/agileworks-tw/RN_Todo_Sample)

練習：
將原本接好後端 API 的 ToDo List App 加上 Redux

1. 安裝 redux, react-redux, remote-redux-devtools 套件
2. 建立 configureStore.js
3. 將 Root Component 設為 Provider
4. 加入 ToDoList 功能相關的 Action, Reducer，將相關的資料處理邏輯移到 reducer 中
5.  使用 connect 方法將 ToDoList Component 連接 Redux Action 和 Store

## 練習前設置

### 下載專案

- ToDoList RESTful API server

```bash
cd ~/workspace
git clone https://github.com/agileworks-tw/express-example
cd express-example
git checkout practice/005002_answer
yarn
```

- ToDoList React Native Sample

```bash
cd ~/workspace
git clone https://github.com/kyoyadmoon/RN_Todo_Sample
cd RN_Todo_Sample
git checkout feature/todo-list-with-api-server
yarn
```

### 回復修改檔案狀態

```bash
git add .
git reset --hard HEAD
```

### 執行專案 （依照順序執行)

Run API server

```bash
cd ~/workspace/express-example
npm start
```

Run React Native ToDoList

```bash
cd ~/workspace/RN_Todo_Sample
# 確認在 feature/add-todo-list branch
# 這會執行 packager server
react-native start
# 需要另外開一個 terminal
react-native run-android
# 模擬器連接 3000 port
adb reverse tcp:3000 tcp:3000
```

完成後應該可以在 android 看到成功畫面

![todo-list-sample-ready](assets/todo-list-sample-ready.png)

## 參考資料

### 練習解答

[https://github.com/agileworks-tw/RN_Todo_Sample/pull/8](https://github.com/agileworks-tw/RN_Todo_Sample/pull/8)
