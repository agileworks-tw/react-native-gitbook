# 生成 App 檔

## 步驟

1.  Static Bundle 打包 JS
2.  將原生專案編譯成 App

## 1. Static Bundle

打包靜態 JS  檔案

### iOS

```bash
react-native bundle --entry-file index.ios.js --platform ios --dev false --bundle-output ios/main.jsbundle --assets-dest ios
```

### android

```bash
react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
```

## 2. 原生專案編譯

### iOS


### android

```bash
cd android && ./gradlew assembleRelease
```
