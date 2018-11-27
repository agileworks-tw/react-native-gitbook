# 熱部署練習

難度： 進階

目標： 整合 react-native-codepush ，透過 appcenter-cli 更新 App 內容

專案： [https://github.com/agileworks-tw/RN_Todo_Sample](https://github.com/agileworks-tw/RN_Todo_Sample)

練習：

1. 安裝 react-native-codepush
2. 設定整合 App Center 應用程式
3. 打包 production App，安裝到模擬器或手機上
4. 修改樣式，並使用 appcenter-cli 更新，查看是否更新成功

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
git checkout feature/async-storage
yarn
```

GitHub Repo: [https://github.com/agileworks-tw/express-example](https://github.com/agileworks-tw/express-example)

切換到 branch `practice/jwt`

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

## 參考資料

### 練習解答

[https://github.com/agileworks-tw/RN_Todo_Sample/pull/15](https://github.com/agileworks-tw/RN_Todo_Sample/pull/15)