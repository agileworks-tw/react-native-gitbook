# 初始化專案 - 新增樣板與專案

## Native module 架構說明

一個支援 Android / iOS 雙平台的 Native Module 專案內應該會包含以下結構：

```.
.
├──android
├──ios
├──index.js
├──package.json
└──README.md
```

## 建立 RN 專案

首先，在開始製作 Native Module 之前，要先手動新建一個 React Native 專案。

這個順序不是必須的，僅在本文介紹流程中需要這麼做，因為我們會先介紹使用 `react-native-cli` 提供的方式建立 module 樣板。

```shell
# 建立 React Native 專案
$ react-native init ReactNativeToast
```

## 使用 react-native-cli 產生樣板

```shell
# 必須在 React Native 專案內才能使用 cli 指令 `new-library`
$ cd ReactNativeToast

$ react-native new-library --name "MyAndroidToast"

# 結果
➜  ReactNativeToast react-native new-library --name "MyAndroidToast"
Scanning folders for symlinks in /Users/kueiyen/_playground/ReactNativeToast/node_modules (11ms)
Created library in /Users/kueiyen/_playground/ReactNativeToast/Libraries/MyAndroidToast
Next Steps:
   Link your library in Xcode:
   https://facebook.github.io/react-native/docs/linking-libraries-ios.html#content
```

- 優點
  - facebook 內建工具，沒有相容問題

- 缺點
  - 只會自動建立 iOS 部分，不支援自動產生 Android 專案
  - 需要手動 link
  - 依賴於目前的 RN 專案，較難拆開單獨發布、維護

---

## 使用 react-native-create-library 產生樣板

> version @ `3.1.2`

### 簡介

`react-native-create-library` 是一個第三方的 React Native Cli 命令列工具，主要負責快速建立 Native module 必要的專案結構。

目前經測試可以正確支援 React Native @ `0.52.2`。

- 優點
  - 支援 Android / iOS / Windows 平台
  - 對於 RN 專案沒有依賴性，可以獨立開發與發佈版本
  - 可以透過指令參數設定平台、模組名稱、package id 等屬性

- 缺點
  - 不支援 UI module 建立，需要手動設定
  - 由於更新時間不一定，所以可能不支援最新的 React Native 版本
  - 由於更新時間不一定，所以某些 native 設定可能需要手動更新

#### 參考

- [frostney/react-native-create-library: Command line tool to create a React Native library with a single command](https://github.com/frostney/react-native-create-library)

### 安裝

```shell
# 注意：需要 node 版本 > 6.0
$ npm install -g react-native-create-library
```

### 指令參數

`react-native-create-library` 支援選項參數，可以用來指定產生的 module 名稱以及 package 名稱等相關資訊。

```shell
Usage: react-native-create-library [選項] <名稱>

Options:

  -h, --help                                顯示說明
  -V, --version                             顯示版本號
  -p, --prefix <prefix>                     指定 library prefix (預設: `RN`)
  --module-prefix <modulePrefix>            指定 library 的 module prefix(預設: `react-native`)
  --package-identifier <packageIdentifier>  (Android only!) Android module 的 package name (預設: `com.reactlibrary`)
  --namespace <namespace>                   (Windows only!) The namespace for the Windows module
   (Default: The name as PascalCase)
  --platforms <platforms>                   工具將會產生哪些平台的樣板 (使用 `,` 逗號分隔; 預設: `ios,android,windows`)
```

預設的 module prefix 是 `react-native`，預設的 library prefix 則是 `RN`，如果給予的名稱是駝峰式命名，則將會自動將大寫與小寫轉換成 `-` 連結。

本教學將製作一個叫做 `MyAndroidToast` 的 module，如果套用預設的參數，那就會產出：

- module name：`react-native-my-android-toast`

這個名稱會作為 npm 套件的 package name 使用，也就是 ***React Native 專案將要 import/reqire 的來源套件名稱***。

- library name：`RNMyAndroidToast`

這個名稱則會 ***作為 native module 被 export 的對象物件***，同時也是 ***React Native 專案將要 import/require 之後的物件名稱***。

例如：

```javascript
// 亦即 import {library_name} from {module_name}
import MyAndroidToast from  'react-native-my-android-toast';
```

> #### 注意！

這裡要非常注意一點，所有的 `prefix` 與樣板內 Android/iOS 專案內所有的 class name 都是依據 `name` 參數產生，所以盡量第一次就決定好名稱，**事後要修改會非常麻煩**。

### 透過指令產生樣板

```shell
# 我們要建立一個叫做 MyAndroidToast 的 module，只有 Android 平台
$ react-native-create-library MyAndroidToast --platforms android

# 結果
➜  root react-native-create-library MyAndroidToast
While `RN` is the default prefix,
  it is recommended to customize the prefix.

📚  Created library MyAndroidToast in `./MyAndroidToast`.
🕘  It took 20ms.
➡️  To get started type `cd ./MyAndroidToast`

# 完成之後，記得要 yarn install
$ cd ./MyAndroidToast && yarn install
```