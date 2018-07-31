# Linking Projects

## 使用 yarn link

假設目前開發中 native module 與 RN 專案的目錄關係如下：

```.
.[root]
├──[react_native_project]
└──[native_module]
```

首先我們要查看 native module 底下的 `package.json`，確認 module package name：

```json=
{
 "name":   "react-native-my-android-toast", <---- 這裡
 "version":   "1.0.0",
 "description":   "",
 "main":   "index.js",
 "scripts":   {
 "test":   "echo \\"Error: no test specified\\" && exit 1"
 },
 "keywords":   [
 "react-native"
 ],
 "author":   "",
 "license":   "",
 "peerDependencies":   {
 "react-native":   "^0.41.2",
 "react-native-windows":   "0.41.0-rc.1"

 }
}
```

由此可以得知，這個 native module 在 npm 套件會被稱為稱為 `react-native-my-android-toast`。


那我們就能透過以下指令，來 link 兩個專案：

- Step-1：進入 native_module 目錄 

```shell
# 進入到存放兩個專案的根目錄
$ cd root

--

# step-1 進入 native_module 目錄
$ cd native_module

# # 單獨使用 link，此動作會像 yarn 註冊這個 node 模組
$ yarn link 
```

```shell
# 結果
➜  MyAndroidToast yarn link
yarn link v1.3.2
warning package.json: License should be a valid SPDX license expression
warning package.json: License should be a valid SPDX license expression
success Registered "react-native-my-android-toast".
info You can now run `yarn link "react-native-my-android-toast"` in the projects where you want to use this module and it will be used instead.
✨  Done in 0.08s.
```

- Step-2 進入 react-native-project 目錄

```shell
# step-2 進入 react-native-project 目錄
$ cd react_native_project

# 進行 link [module_name]，以本教學來說是 "react-native-my-android-toast"
$ yarn link "react-native-my-android-toast"

# 結果
➜  ReactNativeToast yarn link "react-native-my-android-toast"
yarn link v1.3.2
success Using linked module for "react-native-my-android-toast".
✨  Done in 0.06s.
```

- 如果開發完成 ...
 
```shell
# 當 Native module 開發完成後，
# 或要改為使用 npm install 方式安裝時，可透過以下指令取消 link
$ yarn unlink "react-native-my-android-toast"
```
