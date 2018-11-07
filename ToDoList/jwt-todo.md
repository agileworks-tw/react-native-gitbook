# JWT 驗證練習

## 後端專案

GitHub Repo: [https://github.com/agileworks-tw/express-example](https://github.com/agileworks-tw/express-example)

切換到 branch `practice/jwt`

執行

```bash
npm start
```

## 目標

> 切換到 `feature/async-storage` branch

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
  fetch('http://localhost:3000/login', {
    method: 'POST',
    headers: {
      Accept: 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      username: 'rn-tw',
      password: 'rn-tw'
    })
  })
    .then(res => res.json())
    .then(result => console.log(result));
  ```
3. 透過請求的 response 確認是否登入成功  (res.success)，若成功則將 jwt token 寫入 AsyncStorage ， 連同 username 資料一併跳轉至 ToDoList 頁面

4. 依照 JWT 標準將 ToDoList API 頁面的 get, create, delete API 加上 Authorization token，讓 API 可以成功運作

## 範例

範例連結: [https://github.com/agileworks-tw/RN_Todo_Sample/pull/6](https://github.com/agileworks-tw/RN_Todo_Sample/pull/6)
