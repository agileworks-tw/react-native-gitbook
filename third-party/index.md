# 第三方套件管理

## 套件管理工具

- npm
- yarn

### 新增套件到專案

```bash
$ yarn add <Package_Name>@<Version>
ex: yarn add lodash@4.17.0
```

### 包含原生模組的套件

需要將資源和原生程式碼加入到原生專案中

1.  使用 react-native link 自動連結原生模組

```bash
# 1. install package
$ yarn add <Package_Name>

# 2. link package
$ react-native link <Package Name>

# 3. App (Packager server )
$ react-native run-ios
```

2.  手動設定連結

自行將原生模組資源加入原生專案

- [手動設定參考方式](https://facebook.github.io/react-native/docs/linking-libraries-ios.html#manual-linking)

### 移除套件

```bash
# 若 link 過原生模組，需要先做 unlink
$ react-native unlink <Package_Name>

# remove node_module
$ yarn remove <Package_Name>
```

### 整合套件練習

1.  整合 icon 套件 react-native-vector-icons
