# Networking

## Fetch

- 發送 HTTP 請求

- App 與後端 Server 間的溝通方法

- 提供了和 web 標準一至的 Fetch API

- 有用過 AJAX 使用起來就會很上手

- iOS 9、10、11 不支援 http，要使用 https，或是在 Info.plist 設定例外網域

  ```plist
  <key>NSAppTransportSecurity</key>
  <dict>
    <key>NSExceptionDomains</key>
    <dict>
      <key>rn.fuyaode.me</key>
      <dict>
        <key>NSExceptionAllowsInsecureHTTPLoads</key>
        <true/>
      </dict>
      <key>localhost</key>
      <dict>
        <key>NSExceptionAllowsInsecureHTTPLoads</key>
        <true/>
      </dict>
    </dict>
  </dict>
  ```

  ![fetch](./assets/fetch.png)

## 使用教學

### get

```js
getData = async page => {
  try {
    let response = await fetch(`http://rn.fuyaode.me/users/1`);
    let responseJson = await response.json();
    console.log(responseJson);
    this.setState({
      name: responseJson.name
    });
    return responseJson;
  } catch (e) {
    console.error(e);
  }
};
```

```js
getData = page => {
  return fetch('http://rn.fuyaode.me/users/1')
    .then(response => response.json())
    .then(responseJson => {
      return responseJson.name;
    })
    .catch(error => {
      console.error(error);
    });
};
```

### post

```js
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    firstParam: 'yourValue',
    secondParam: 'yourOtherValue'
  })
});
```

### form

```js
const formData = new FormData();
form.append('id', 'A123123123');
form.append('password', '0000');
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'multipart/form-data'
  },
  body: formData
});
```

### 檔案上傳

- react-native-image-picker: [https://github.com/react-community/react-native-image-picker](https://github.com/react-community/react-native-image-picker) - 選擇圖片、影片套件
- react-native-fs: [https://github.com/itinance/react-native-fs](https://github.com/itinance/react-native-fs) - 檢查檔案大小、判斷檔案是否存在

```js
const formData = new FormData();
form.append('file', {
  uri: filePath,
  name: fileName
});
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'multipart/form-data'
  },
  body: formData
});
```

## WebSocket

全雙工，server 端能發訊息給 client 端，傳統 http 只能用 long polling 從 client 端去跟 server 要資料

```js
var ws = new WebSocket('ws://host.com/path');

ws.onopen = () => {
  // connection opened
  ws.send('something'); // send a message
};

ws.onmessage = e => {
  // a message was received
  console.log(e.data);
};

ws.onerror = e => {
  // an error occurred
  console.log(e.message);
};

ws.onclose = e => {
  // connection closed
  console.log(e.code, e.reason);
};
```

## 延伸閱讀

API: [https://goo.gl/tgXs0J](https://goo.gl/tgXs0J)  
REST: [https://goo.gl/6rXqw](https://goo.gl/6rXqw)  
RESTful API 設計指南: [https://goo.gl/KpKEvS](https://goo.gl/KpKEvS)

- GET（SELECT）：從 server 取出資源（一項或多項）。
- POST（CREATE）：在 server 新建一個資源。
- PUT（UPDATE）：在 server 更新資源（客戶端提供改變後的完整資源）。
- PATCH（UPDATE）：在 server 更新資源（客戶端提供改變的屬性）。
- DELETE（DELETE）：從 server 刪除資源。

WebSocket: [https://goo.gl/syksQp](https://goo.gl/syksQp)
