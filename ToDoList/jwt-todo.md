# JWT 驗證練習

難度： 進階

目標： 加上登入功能與 JWT 驗證

專案： [https://github.com/agileworks-tw/RN_Todo_Sample](https://github.com/agileworks-tw/RN_Todo_Sample)

練習：

1. SignIn 畫面加入 password 輸入欄位
2. Sign in 時送出 `localhost:3000/login` API

```js
// type: 'POST'
// body:
{
  "username": "rn-tw",
  "password": "rn-tw"
}
```

request 範例

```js
fetch("http://localhost:3000/login", {
  method: "POST",
  headers: {
    Accept: "application/json",
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    username: "rn-tw",
    password: "rn-tw"
  })
})
  .then(res => res.json())
  .then(result => console.log(result));
```

3. 透過請求的 response 確認是否登入成功 (res.success)，若成功則將 jwt token 寫入 AsyncStorage ， 連同 username 資料一併跳轉至 ToDoList 頁面

4. 依照 JWT 標準將 ToDoList API 頁面的 get, create, delete API 加上 Authorization token，讓 API 可以成功運作

## 練習前設置

### 下載專案

- ToDoList RESTful API server

```bash
cd ~/workspace
git clone https://github.com/agileworks-tw/express-example
cd express-example
git checkout practice/jwt
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

### 回復修改檔案狀態

```bash
git add .
git reset --hard HEAD
```

### 執行專案 （依照順序執行)

#### Run API server

```bash
cd ~/workspace/express-example
npm start
```

#### Run React Native ToDoList

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

[https://github.com/agileworks-tw/RN_Todo_Sample/pull/6](https://github.com/agileworks-tw/RN_Todo_Sample/pull/6)
