# Linking Projects

## 使用 react-native link

`react-native-cli` 中封裝了 `rnpm` 的指令 `link`，它可以自動幫我們在 native code 的部分新增必備的程式碼，例如告訴 Android 專案它該去哪裡存取 native module 的相關資訊。

> ### 注意！
> 如果你的 Native module 沒有引入其他 native module，那就不必額外做這一段的處理

> ### 注意！
> 如果你使用 `yarn link` 之後 `push` 到 git 服務，然後 `pull` 下來到別的路徑或是別台電腦，你就會需要重新 `yarn link`；或是，你可以選擇直接使用寫入相對路徑的方式來 link module 與專案，但這樣你每次更新 module 都要清除 `node_module` 資料夾，並且重新`npm install` 以取得最新的更新。

在使用它之前，我們必須手動在 React Native 專案根目錄下的 `package.json` 新增你的 naive module 位置資訊，如果你的專案結構維持與我一樣，如下表：

```.
.[root]
├──[react_native_project]
└──[native_module]
```

那你可以在 `package.json` 的 `dependencies` 部分新增以下資訊，以供 `react-native link` 讀取 native module 目錄內容使用。

但還記得嗎？由於是透過 `yarn link` 連結兩個專案，我們並非由 `package.json` 所指定的目錄取得該 module 內容，所以完成後必須移除此行資訊。

```json
"react-native-my-android-toast":   "file:../MyAndroidToast",
```

完整檔案內容如下：

```json
{
  "name": "ReactNativeToast",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start",
    "test": "jest"
  },
  "dependencies": {
    "react": "16.2.0",
    "react-native-my-android-toast": "file:../MyAndroidToast", <--- 這裡
    "react-native": "0.52.2"
  },
  "devDependencies": {
    "babel-jest": "22.1.0",
    "babel-preset-react-native": "4.0.0",
    "jest": "22.1.4",
    "react-test-renderer": "16.2.0"
  },
  "jest": {
    "preset": "react-native"
  }
}
```

先前我們已經確認 native module name 為 `react-native-my-android-toast`，所以請切換到專案根目錄，執行以下指令：

```shell
# 切換到專案根目錄
$ cd ReactNativeToast

# 執行 link ${module_name}
$ react-native link react-native-my-android-toast

# 結果
➜  ReactNativeToast react-native link react-native-my-android-toast
Scanning folders for symlinks in /Users/kueiyen/_playground/ReactNativeToast/node_modules (12ms)
rnpm-install info Linking react-native-my-android-toast android dependency
rnpm-install info Android module react-native-my-android-toast has been successfully linked
```

> ### 注意！
> 請記得一定要在 `react-native link` 後接上 native module 名稱，避免意外 link 了不想要/不需要的專案。

完成後如果使用 Android Studio 開啟專案，會發現 `react-native link` 自動幫我們在這些地方新增了程式碼：

- MainApplication.java

![](https://i.imgur.com/zMy8eRM.png)

- build.gradle

![](https://i.imgur.com/cDiS75w.png)

- settings.gradle

![](https://i.imgur.com/p8lLihQ.png)

由上面案例可以了解 native module 時命名必須全部統一，否則使用 `react-native link` 指令可能會有問題。

> #### 注意！
> 在 `react-native link` 完成後，請記得移除剛才在 `package.json` 中新增的一行資訊。否則下次 `yarn install` or `npm install` 會取得錯誤的套件資訊，導致不能執行專案。
