# Facebook 登入整合

## SDK 套件整合

### 安裝

[Github Repo: https://github.com/facebook/react-native-fbsdk](https://github.com/facebook/react-native-fbsdk)

安裝 0.7.0 版本

```bash
npm install react-native-fbsdk@0.7.0
react-native link react-native-fbsdk
```

### 設定整合

#### iOS

確認有最新版本的 Xcode
跟著 [Getting Started Guide: https://developers.facebook.com/docs/ios/getting-started/](https://developers.facebook.com/docs/ios/getting-started/)步驟整合 Facebook 應用程式 SDK
別忘了將 `FBSDKShareKit.framework` and `FBSDKLoginKit.framework` 加到原生專案中

#### Android

`MainApplication.java`　檔案
首先加入 CallbackManager
如下：

```java
import com.facebook.CallbackManager;
import com.facebook.FacebookSdk;
import com.facebook.reactnative.androidsdk.FBSDKPackage;
import com.facebook.appevents.AppEventsLogger;
...

public class MainApplication extends Application implements ReactApplication {

  private static CallbackManager mCallbackManager = CallbackManager.Factory.create();

  protected static CallbackManager getCallbackManager() {
    return mCallbackManager;
  }
  //...
```

覆寫 onCreate() method

```java
@Override
public void onCreate() {
  super.onCreate();
  AppEventsLogger.activateApp(this);
  //...
}
```

在 getPackages() 註冊 SDK package

```java
private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
    @Override
    public boolean getUseDeveloperSupport() {
      return BuildConfig.DEBUG;
    }

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new FBSDKPackage(mCallbackManager)
      );
    }
};
```

---

`MainActivity.java`　檔案
覆寫 onActivityResult() method

```java
import android.content.Intent;

public class MainActivity extends ReactActivity {

    @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        MainApplication.getCallbackManager().onActivityResult(requestCode, resultCode, data);
    }
    //...
```

---

`setting.gradle` 檔案
(這部分 link 應該處理過了，可以確認一下)

```gradle
include ':react-native-fbsdk'
project(':react-native-fbsdk').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-fbsdk/android')
```

接下來跟著  [Getting Started Guide: https://developers.facebook.com/docs/android/getting-started/](https://developers.facebook.com/docs/android/getting-started/) 的 Facebook 應用程式 SDK 整合步驟做（build.gradle 的部分可以跳過，react-native link 已經處理了），不要漏掉 `strings.xml`, `AndroidManifest.xml` 的相關設定

### 使用

#### 官方 LoginButton 元件

```javascript
import React, { Component } from 'react';
import { View } from 'react-native';
import { LoginButton, AccessToken } from 'react-native-fbsdk';

export default class Login extends Component
  render() {
    return (
      <View>
        <LoginButton
          onLoginFinished={
            (error, result) => {
              if (error) {
                console.log("login has error: " + result.error);
              } else if (result.isCancelled) {
                console.log("login is cancelled.");
              } else {
                // 登入成功取得 AccessToken
                AccessToken.getCurrentAccessToken().then(
                  (data) => {
                    console.log(data.accessToken.toString())
                  }
                )
              }
            }
          }
          onLogoutFinished={() => console.log("logout.")}/>
      </View>
    );
  }
});
```

#### 透過 LoginManager 登入請求額外權限

```javascript
import { LoginManager } from 'react-native-fbsdk';
// ...

// Attempt a login using the Facebook login dialog asking for default permissions.
LoginManager.logInWithReadPermissions(['public_profile']).then(
  function(result) {
    if (result.isCancelled) {
      console.log('Login cancelled');
    } else {
      console.log(
        'Login success with permissions: ' +
          result.grantedPermissions.toString()
      );
    }
  },
  function(error) {
    console.log('Login fail with error: ' + error);
  }
);
```

#### Graph API

若要拿到 Facebook 的相關資料需要登入之後，透過 Graph API 取得

```js
import { GraphRequest, GraphRequestManager } from 'react-native-fbsdk';

// ...

//Create response callback.
_responseInfoCallback(error: ?Object, result: ?Object) {
  if (error) {
    console.log('Error fetching data: ' + error.toString());
  } else {
    console.log('Success fetching data: ' + result.toString());
  }
}

// Create a graph request asking for user information with a callback to handle the response.
const infoRequest = new GraphRequest(
  '/me',
  null,
  this._responseInfoCallback,
);
// Start the graph request.
new GraphRequestManager().addRequest(infoRequest).start();
```

