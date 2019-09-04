# 初始化專案

## 修正樣板 Gradle 版本

### 使用 Android Studio 開啟樣板專案

由於我們的目標是撰寫一套可以使用原生 Android `Toast` 功能的 native nodule，所以我們需要透過 Android Studio 打開專案資料夾中的 `android` 目錄。

```.
.
├──android     --------> Android 專案目錄
├──ios         --------> iOS 專案目錄
├──index.js    --------> React Native 進入點，也可依據平台分為 index.android.js / index.ios.js
├──package.json
└──README.md
```

在當前版本，使用 `Android Studio` 打開專案時，應該會看到如下圖的詢問視窗，請點選 `OK`。

這是因為樣板並沒有包含 Android 專案所需要的 gradle 相關套件，所以我們需要讓它自動取得。

![](https://i.imgur.com/KSQANOp.png)

### 修正樣板 Gradle 版本

如果你跟我使用相同版本，在某些情況下，你可能會遇到跟我一樣的問題：Android Studio 提示樣板需要使用不同的 Gradle 版本。

這是因為系統中沒有樣板指定的 Gradle 版本，我們需要手動修正這個問題。

![](https://i.imgur.com/ACayr5B.png)

找到左側樹狀目錄中的 `Gradle Scripts`，點選第一個 `build.gradle`，它應該長得像這樣：

```
build.gradle(Module: android)
```

開啟後可由下圖中發現，目前樣板內指定的版本為：

```gradle=
classpath 'com.android.tools.build:gradle:`1.3.1`'
```

![](https://i.imgur.com/MEddIki.png)

目前（2018/02）最新的 Gradle 已經來到 `4.5`；而 Android Studio 使用的對應版本可以參照這個連結：([Android Plugin for Gradle Release Notes | Android Studio](https://developer.android.com/studio/releases/gradle-plugin.html#updating-gradle)) --- 簡單來說，我們需要修改對應的 Gradne 以及 Android Plugin 版本，而**這些版本最好跟著你的 React Native 專案的版本同步**。

依據文件說明，版本更新 Gradle 版本可以帶來巨大的好處：編譯專案時間會顯著減少。但是如果 Native module 使用的版本與 React Native 專案不同或相差太大，可能會有額外的問題產生。

### 手動更新 Gradle 與 Android Plugin 版本

依據文件說明，我們可以透過 `Project Strucature` 選單內的 `Proejct` 頁籤設定 Gradle 與 Android Plugin 版本。

![](https://i.imgur.com/dP3wm15.png)

我們可以透過以下快速鍵呼叫該選單：

###### [!] 參考 [Keyboard Shortcuts | Android Studio](https://developer.android.com/studio/intro/keyboard-shortcuts.html)

- Windwos：`Control + Alt + Shift + S`
- Mac：`Command + ;`

然後找到左側的 `Project` 頁籤，更改對應的欄位，如下所示。如此一來，我們就會有與 React Native 0.52.2 相同的版本設定。

- Gradle version : [`2.14.1`] 
- Android Plugin Version : [`2.2.3`] // 注意小數點版本號必須完全相符

接下來，再次打開 `build.gradle`，。

![](https://i.imgur.com/X8J2jm8.png)

找到 `repositories` 區段，修改內容如下：

```gradle
repositories {  
   mavenCentral()  
   maven {  
   // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm  
   url "$rootDir/../node_modules/react-native/android"  
   }  
   maven {  
   url 'https://maven.google.com/'  
   name 'Google'  
   }  
}
```

最後應該會像下圖這個樣子：

![](https://i.imgur.com/pKPLfpq.png)
