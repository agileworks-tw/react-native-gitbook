# 實作 Wifi Module

## 取得權限

需要打開檔案 `AndroidManifest.xml`，在 `<manifest>
` 標籤內加入以下兩行，以便後續取得 Wifi 的控制權限：

```xml=
<!-- 取得 wifi 操作權限 -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```

## 實作 MyWifiManager

由於 Android 的 `WifiManager` 提供很多複雜功能，所以我們需要額外封裝它，請新增一支 `MyWifiManager.java`，內容如下：

```java
public class MyWifiManager {
    private WifiManager mWifiManager;
    private WifiInfo mWifiInfo;

    public MyWifiManager(Context context) {
        mWifiManager = (WifiManager) context.getApplicationContext().getSystemService(Context.WIFI_SERVICE);

        mWifiInfo = mWifiManager != null ? mWifiManager.getConnectionInfo() : null;
    }

    // 檢查並取得目前 WIFI 狀態
    public int getState(Context context) {
        if (mWifiManager.getWifiState() == WifiManager.WIFI_STATE_DISABLING) {
            Toast.makeText(context, "Wifi 關閉中...", Toast.LENGTH_SHORT).show();
        } else if (mWifiManager.getWifiState() == WifiManager.WIFI_STATE_DISABLED) {
            Toast.makeText(context, "Wifi 已經關閉", Toast.LENGTH_SHORT).show();
        } else if (mWifiManager.getWifiState() == WifiManager.WIFI_STATE_ENABLING) {
            Toast.makeText(context, "Wifi 正在開啟...", Toast.LENGTH_SHORT).show();
        } else if (mWifiManager.getWifiState() == WifiManager.WIFI_STATE_ENABLED) {
            Toast.makeText(context, "Wifi已经开启", Toast.LENGTH_SHORT).show();
        } else {
            Toast.makeText(context, "没有获取到WiFi状态", Toast.LENGTH_SHORT).show();
        }
        return mWifiManager.getWifiState();
    }
}
```

### 在 RNMyWifiModuleModule 初始化 MyWifiManager

```java
  // 在建構子初始化 MyWifiManager
  public RNMyWifiModuleModule(ReactApplicationContext reactContext) {
      super(reactContext);
      this.reactContext = reactContext;
      this.wifiManager = new MyWifiManager(reactContext);
  }
```

### 新增 getWifiStatus() 方法

#### Native module 如何接收回傳

有三種方式可以回傳來自 native code 層級的資訊或物件，如下：

- Callback
- Promises
- Event

其中 `Callback` 與 `Promises` 類似，由於我們使用 Node v8 系列已經支援 `async/await` 方法，所以我們會統一在 Java code 部分使用 `Promises` 方式，搭配在 JavaScript 端使用 `async/await`，以求簡潔。

如果針對 JavaScript 的 ES2016(ES7) 標準的 async/await 不熟悉，建議先了解相關文件或書籍。

#### 使用 Promises

```java
  // 製作一個 Promise 函式，使我們可以把 Android 資訊回傳到 JavaScript 端，
  // 並在 JS 端使用 async/await 方式來取得資訊
  // e.g. => const status = await MyWifiManager.getWifiStatus();
  // *Promise 來自 React Native 提供的 com.facebook.react.bridge.Promise 套件
  @ReactMethod
  public void getWifiStatus(Promise promise) {
      try {
          // 回傳狀態
          int statusCode = this.wifiManager.getState(reactContext);
          WritableMap map = Arguments.createMap();
          promise.resolve(statusCode);
      } catch (Exception e) {
          promise.reject(e.getMessage());
      }
  }
```

#### 使用 Event

首先新增一個 `sendEvent()` 方法，用來統一發送事件到 JS 端。

```java
  // 製作一個可以主動發送事件到 JS 端的接口
  // eventName ==> Event Key
  private void sendEvent(String eventName,
                          @Nullable WritableMap params) {
      if (reactContext.hasActiveCatalystInstance()) {
          reactContext
                  .getJSModule(DeviceEventManagerModule.RCTDeviceEventEmitter.class)
                  .emit(eventName, params);
      }
  }
```

然後，我們需要新增另外一個方法，用來發送 Wifi status code：

```java
  @ReactMethod
  public void getWifiStatusByEvent(Promise promise) {
      // 回傳狀態
      int statusCode = this.wifiManager.getState(reactContext);
      WritableMap map = Arguments.createMap();
      map.putInt("statusCode", statusCode);
      sendEvent("WIFI_STATUS", map);
  }
```

### Export native module

```javascript
import { NativeModules, DeviceEventEmitter } from 'react-native';

const { RNMyWifiModule } = NativeModules;

// 如果 export 的 native module package 有多個 module，
// 可以在這裡指定哪個 function 呼叫哪個 module method
RNMyWifiModule.getWifiStatus = RNMyWifiModule.getWifiStatus;

// 定義事件 key-map
const eventsMap = {
  WIFI_STATUS: 'WIFI_STATUS',
};

// 定義 Event Listener function，可以在 RN 專案內使用
RNMyWifiModule.on = (event, callback) => {
  const nativeEvent = eventsMap[event];
  if (!nativeEvent) {
    throw new Error('@index.js: Invalid event');
  }
  DeviceEventEmitter.removeAllListeners(nativeEvent);
  return DeviceEventEmitter.addListener(nativeEvent, callback);
}

export default RNMyWifiModule;
```

### React Native 端使用套件

首先在 `App.js` 最前端引入此套件：

```javascript
// 引入 RNMyWifiModule
import RNMyWifiModule from 'react-native-my-wifi-module';
```

為了要顯示 `Alert`、以及使用 `Button` 呼叫 native module 功能，所以記得把 `import ... from React` 修改為如下：

```javascript
import {
  Alert,
  Button,
  Platform,
  StyleSheet,
  Text,
  View
} from 'react-native';
```

然後在 class `App` 內新增 `componentDidMount` 方法，用來註冊 event 監聽器：

```javascript
  componentDidMount() {
    RNMyWifiModule.on('WIFI_STATUS', (data) => {
      Alert.alert('WIFI_STATUS', JSON.stringify(data));
    });
  }
```

同時，我們需要建立兩個按鈕與對應事件，分別對應剛才建立的 native module 方法 `getWifiStatusByEvent()` 與 `getWifiStatus()`：

```javascript
  componentDidMount() {
    RNMyWifiModule.on('WIFI_STATUS', (data) => {
      Alert.alert('WIFI_STATUS', JSON.stringify(data));
    });
  }

  getWifiStatusByEvent = () => {
    // 由於是 event，所以不需要 async/await，但需要註冊監聽事件
    const status = RNMyWifiModule.getWifiStatusByEvent();
  }

  getWifiStatus = async () => {
    // 由於是封裝 Promises，所以需要使用 async function 以及使用 await 前輟
    // 該 metod 會非同步地直接回傳值
    const status = await RNMyWifiModule.getWifiStatus();
    Alert.alert('getWifiStatus', `getWifiStatus=>${status}`);
  }
```

接下來，我們需要在 view 建立按鈕：

```javascript
  render() {
    return (
      <View style={styles.container}>
        <Button title='Get Wifi Status!' onPress={this.getWifiStatus}/>
        <Button title='Get Wifi Status by EVENT!' onPress={this.getWifiStatusByEvent}/>
      </View>
    );
  }
}
```

![](https://i.imgur.com/w1m3KeI.png)
