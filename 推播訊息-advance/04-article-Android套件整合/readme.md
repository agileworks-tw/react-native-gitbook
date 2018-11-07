## 套件

`react-native-firebase` 

GitHub: [https://github.com/invertase/react-native-firebase](https://github.com/invertase/react-native-firebase)

文件: [https://rnfirebase.io/docs](https://rnfirebase.io/docs)

## 安裝

```bash
npm install --save react-native-firebase
react-native link react-native-firebase
```

## 整合

### Basic

1. 下載 Firebase 專案 Android 應用程式的 `google-services.json`，並將檔案放到 `android/app/google-services.json`

2. 編輯 `android/build.gradle`

   ```java
   buildscript {
     // ...
     dependencies {
       // ...
       classpath 'com.google.gms:google-services:4.0.1'
     }
   }
   ```

3. 編輯 `android/app/build.gradle` 
   最下方加入
   ```java
   apply plugin: 'com.google.gms.google-services'
   ```
   找到 `dependencies` 區塊
   ```java
   dependencies {
     // This should be here already
     implementation project(':react-native-firebase')
   
     // Firebase dependencies
     implementation "com.google.android.gms:play-services-base:16.0.1"
     implementation "com.google.firebase:firebase-core:16.0.4"
   
     ...
   }
   ```

4. #### 更新 Gradle

   ##### 編輯 `android/gradle/wrapper/gradle-wrapper.properties` 

   更新 gradle URL 版本到 `gradle-4.4-all.zip`

   ```
   distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip
   ```

   ##### 編輯 `android/build.gradle`

   找到下面區塊，加入 `google()`

   ```java
   buildscript {
       repositories {
           google()  // <-- Check this line exists and is above jcenter
           jcenter()
           // ...
       }
       // ...
   }
   ```

   更新 Android build tools version `3.2.0`

   ```java
   classpath 'com.android.tools.build:gradle:3.2.0'
   ```

   ##### 編輯 `android/app/build.gradle`，將 `compile` 都替換成 `implementation`

   ```java
   implementation project(':react-native-firebase')
   ```

5. Update Google Play service maven repository
   編輯 `android/build.gradle`

   ```java
   allprojects {
       repositories {
           mavenLocal()
           google() // <-- Add this line above jcenter
           jcenter()
           maven {
               // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
               url "$rootDir/../node_modules/react-native/android"
           }
       }
   }
   ```

### Messaging Module

參考: [https://rnfirebase.io/docs/v5.x.x/messaging/ios](https://rnfirebase.io/docs/v5.x.x/messaging/ios)



編輯 `android/app/build.gradle`

```java
dependencies {
  // ...
  implementation "com.google.firebase:firebase-messaging:17.3.4"
  implementation 'me.leolin:ShortcutBadger:1.1.21@aar' // <-- Add this line if you wish to use badge on Android
}
```

編輯 `android/app/src/main/java/com/[app name]/MainApplication.java`

```java
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.messaging.RNFirebaseMessagingPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseMessagingPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```

編輯 `android/app/src/main/AndroidManifest.xml`

```xml
<application ...>
  <service android:name="io.invertase.firebase.messaging.RNFirebaseMessagingService">
    <intent-filter>
      <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
  </service>
  <service android:name="io.invertase.firebase.messaging.RNFirebaseInstanceIdService">
    <intent-filter>
      <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter>
  </service>
  
  <!-- If you want to be able to react to data-only messages when your app is in the background -->
  <service android:name="io.invertase.firebase.messaging.RNFirebaseBackgroundMessagingService" />
</application>
```



### Notification Module

參考: [https://rnfirebase.io/docs/v5.x.x/notifications/ios



編輯 `android/app/src/main/java/com/[app name]/MainApplication.java`

```
// ...
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.notifications.RNFirebaseNotificationsPackage; // <-- Add this line

public class MainApplication extends Application implements ReactApplication {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNFirebasePackage(),
          new RNFirebaseNotificationsPackage() // <-- Add this line
      );
    }
  };
  // ...
}
```



編輯：`android/app/src/main/AndroidManifest.xml`

```xml
<manifest ...>
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
  <uses-permission android:name="android.permission.VIBRATE" />
  ...
  <application...>
    <meta-data
        android:name="com.google.firebase.messaging.default_notification_channel_id"
        android:value="@string/default_notification_channel_id"/>
  	<activity
  	  ...
	  android:launchMode="singleTop"
	>
      ...
    </activity>
  </application>
</manifest>
```

設定推播通知顏色及 icon (Option)

```xml
<application ...>
  <!-- Set custom default icon. This is used when no icon is set for incoming notification messages.
       See README(https://goo.gl/l4GJaQ) for more. -->
  <meta-data
    android:name="com.google.firebase.messaging.default_notification_icon"
    android:resource="@drawable/ic_stat_ic_notification" />
  <!-- Set color used with incoming notification messages. This is used when no color is set for the incoming
       notification message. See README(https://goo.gl/6BKBk7) for more. -->
  <meta-data
    android:name="com.google.firebase.messaging.default_notification_color"
    android:resource="@color/colorAccent" />
</application>
```

