# Geolocation 地理定位資訊

React Native 的 Geolocation API 依照 [Web 標準: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation)

透過 Geolocation API 可以取得經緯度位置

## 原生專案設定

分別對 iOS、Android 原生專案進行取得位置資訊的權限設定

### iOS

在 `Info.plist` 中增加

```plist
NSLocationWhenInUseUsageDescription
```

> 透過 `react-native init` 初始化的專案是已經預設有這個欄位的

#### 背景 Geolocation 更新

如果需要設定在 App 背景更新 Geolocation

1. 在 `Info.plist` 另外設定 key `NSLocationAlwaysUsageDescription`
2. 打開 Xcode，找到 Tab `Capabilities` 設定 `Background Modes`  為 ON， 並勾選子項目 `Location updates`

### Android

在 `android/app/src/main/AndroidManifest.xml` 檔案中加入這行

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

- 如果 Android 裝置的 API 版本 >= 18 (Android 4.3 以上)
  - 取得的位置資訊還會包含額外的 boolean 值資料 `mocked`，表示此位置資訊可能是由某個服務模擬得出的。
- 如果 Android 裝置的 API 版本 >= 18 (Android 6.0 以上)
  - 則需要額外使用 `PermissionsAndroid API` [https://facebook.github.io/react-native/docs/permissionsandroid.html](https://facebook.github.io/react-native/docs/permissionsandroid.html) 来檢查 `ACCESS_FINE_LOCATION` 權限。 不這麼做可能會導致應用程式閃退。

## API

### requestAuthorization

請求允許取得位置資訊權限

```js
geolocation.requestAuthorization();
```

在 iOS 系統中 ，如果 `Info.plist` 有設定 `NSLocationAlwaysUsageDescription` 訊息，則會用此訊息向使用者請求  `Always` 取得位置資訊的權限 

若是 `Info.plist` 中設定的是  `NSLocationWhenInUseUsageDescription`，則會向使用者請求  `InUse` 取得位置資訊的權限 

### getCurrentPosition

```js
geolocation.getCurrentPosition(geo_success, [geo_error], [geo_options]);
```

取得成功時會呼叫 `geo_success` callback function，並且會將最新取得的位置資訊作為參數傳入 callback function 中

```js
// geo_success callback function 收到的參數 Object
{
  "mocked": false,
  "timestamp": 1540416546058,
  "coords": {
    "speed": 0,
    "heading": 0,
    "accuracy": 22.101999282836914,
    "longitude": 120.5781344,
    "altitude": 0,
    "latitude": 24.1210115
  }
}
```

錯誤時則會呼叫 `geo_error` callback function

`geo_options`

- timeout (ms)
- maximumAge (ms)
  - 快取時間
- enableHighAccuracy (bool)
  - 是否使用  GPS 取得位置資訊，如果是 false 則會給予 WIFI location 資訊
