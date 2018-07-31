# Fetch

- 發送 HTTP 請求
- App 與後端 Server 間的溝通方法
- 提供了和 web 標準一至的 Fetch API
- 有用過 AJAX 使用起來就會很上手

## 使用教學

### get

```
getData = async (page) => {
  try {
    let response = await fetch(`http://rn.fuyaode.me/users/1`);
    let responseJson = await response.json();
    console.log(responseJson);
    this.setState({
      name: responseJson.name
    })
    return responseJson;
  } catch (e) {
    console.error(e);
  }
}
```

```
getData = (page) => {
  return fetch('http://rn.fuyaode.me/users/1')
    .then((response) => response.json())
    .then((responseJson) => {
      return responseJson.name;
    })
    .catch((error) => {
      console.error(error);
    });
}
```

### post

```
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    firstParam: 'yourValue',
    secondParam: 'yourOtherValue',
  }),
});
```

### form

```
const formData = new FormData();
form.append('id', 'A123123123');
form.append('password', '0000');
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'multipart/form-data',
  },
  body: formData,
});
```

### 檔案上傳

- [react-native-image-picker](https://github.com/react-community/react-native-image-picker) - 選擇圖片、影片套件  
- [react-native-fs](https://github.com/itinance/react-native-fs) - 檢查檔案大小、判斷檔案是否存在  

```
const formData = new FormData();
form.append('file', {
  uri: filepath,
  name: fileName,
});
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'multipart/form-data',
  },
  body: formData,
});
```

## 延伸閱讀

[API](https://zh.wikipedia.org/wiki/%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E6%8E%A5%E5%8F%A3)  
[REST](https://zh.wikipedia.org/wiki/REST)  
[RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)  

- GET（SELECT）：從 server 取出資源（一項或多項）。
- POST（CREATE）：在 server 新建一個資源。
- PUT（UPDATE）：在 server 更新資源（客戶端提供改變後的完整資源）。
- PATCH（UPDATE）：在 server 更新資源（客戶端提供改變的屬性）。
- DELETE（DELETE）：從 server 刪除資源。  

[WebSocket