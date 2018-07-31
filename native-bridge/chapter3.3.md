# Linking Projects

## 疑難解答 - 有問題嗎？

有時候開發 Native module 時會遇到明明已經 `yarn link`、也已經 `react-native link`，build 也正常，但使用 console.log 查看 module 內容卻都是 `undefinded`。

> ### 注意 1
> 首先，確認是否使用了 `yarn link` 之後還在 `package.json` 中新增了 native module 的路徑，這樣會導致錯誤、衝突，一團混亂。

> ### 注意 2
> 要記得確保 Android Studio **沒有任何需要 Sync Gradle 的提示**。

> ### 注意 3
> 每次改完 native module，都要使用 Android Studio 執行選單 Build -> `rebuild`，然後重新透過 `react-native run-android` 來 deply 到 device，否則 React Native Packager 會提示找不到你的 native module。

> #### 小提醒
> 在製作 native module 時，建議同時使用 `Android Studio` 開啟 module 與  RN 專案兩個目錄，除了可以使用 `logcat` 偵錯之外，如果有任何指令下錯、link 錯誤，都可以由 `Android Studio` 直接獲得提醒。

無論是否忘記在 `package.json` 中移除先前新增的套件路徑，我們這時候可以試著透過清除 React Native 的環境快取以及重新 link 彼此來解決問題。

先確認 RN 專案與 Native module 目錄關係如下：

```.
.[root]
├──[react_native_project]
└──[native_module]
```

```shell

# Step-1
# 先切換到 native_module 目錄下
$ cd root/${native_module}

# 需要先 unlink 再 link
$ yarn unlink && yarn link

# Step-2
# 切換回 RN 專案目錄
$ cd ../react_native_project

# yarn unlink ${native_module_name}
$ yarn unlink react-native-my-android-toast

# 清除快取並重新 install node packages
$ watchman watch-del-all && rm -rf $TMPDIR/react-* && rm -rf node_modules/ && yarn install

# 重新 yarn link ${native_module_name}
$ yarn link react-native-my-android-toast

# 再次安裝
$ react-native run-android
```
