# 練習整合 Facebook 登入

難度： 進階

目標： 整合 Facebook 第三方登入功能

專案： [https://github.com/agileworks-tw/RN_Todo_Sample](https://github.com/agileworks-tw/RN_Todo_Sample)

練習：
將原本接好後端 API 的 ToDo List App 加上 Redux

1. 安裝 react-native-fbsdk
2. 設定 facebook app 整合
3. 新增 LoginButton 做 FB 登入
4. 透過 Graph API 取得 Facebook 使用者名稱，並將名稱作為參數跳轉到 todolist 畫面

## 練習前設置

### 下載專案

- ToDoList React Native Sample

```bash
cd ~/workspace
git clone https://github.com/kyoyadmoon/RN_Todo_Sample
cd RN_Todo_Sample
git checkout feature/async-storage
yarn
```

> 如果想跳過套件整合設置
> ```bash
> git checkout 34a46e2
> yarn
> ```


### 回復修改檔案狀態

```bash
git add .
git reset --hard HEAD
```

### 執行專案 （依照順序執行)

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

## 參考資料

### 練習解答

[https://github.com/agileworks-tw/RN_Todo_Sample/pull/5](https://github.com/agileworks-tw/RN_Todo_Sample/pull/5)
