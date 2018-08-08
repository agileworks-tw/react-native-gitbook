# 整合包含原生模組的套件

需要將資源和原生程式碼加入到原生專案中

1.  使用 react-native link 自動連結原生模組

```bash
# 1. install package (沒有 yarn 也可以使用 npm 進行安裝，參考上個章節的指令)
$ yarn add <Package_Name>

# 2. link package
$ react-native link <Package Name>

# 3. App (Packager server )
$ react-native run-ios
```

2.  手動設定連結

自行將原生模組資源加入原生專案

- 手動設定參考方式: [https://facebook.github.io/react-native/docs/linking-libraries-ios.html#manual-linking](https://facebook.github.io/react-native/docs/linking-libraries-ios.html#manual-linking)

## 移除套件

```bash
# 若 link 過原生模組，需要先做 unlink
$ react-native unlink <Package_Name>

# remove node_module
$ yarn remove <Package_Name>
```
