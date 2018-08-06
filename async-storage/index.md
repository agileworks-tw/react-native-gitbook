# AsyncStorage - App 儲存空間

## AsyncStorage 介紹

- 無加密
- key-value 格式
- key 和 value 皆為字串格式
- 在 App 中是全域的
- App 移除後，AsyncStorage 也會清除
- 以非同步方式存取，使用 Promise 包裝

## API

官方文件: [https://facebook.github.io/react-native/docs/asyncstorage.html](https://facebook.github.io/react-native/docs/asyncstorage.html)

- setItem
- getItem
- mergeItem
- removeItem
- clear

## 使用方法

```javascript
import { AsyncStorage } from 'react-native';
const APP_STORAGE_KEY = 'APP_STORAGE_KEY';
async function example() {
  // 寫入資料到 AsyncStorage
  await AsyncStorage.setItem(APP_STORAGE_KEY, 'Hello');
  // 從 AsyncStorage 讀取資料
  const data = await AsyncStorage.getItem(APP_STORAGE_KEY);
  // data: 'Hello'
}
```

## Sample

AsyncStorage Sample: [https://snack.expo.io/@dmoon/asyncstorage-sample](https://snack.expo.io/@dmoon/asyncstorage-sample)
