# 生成 App 檔

## 步驟

1.  Static Bundle 打包 JS
2.  將原生專案編譯成 App

## 1. Static Bundle

打包靜態 JS 檔案

### iOS

```bash
react-native bundle --entry-file index.js --platform ios --dev false --bundle-output ios/main.jsbundle --assets-dest ios
```

### android

```bash
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
```

## 打包問題

### React Native 0.60 Android Duplicate resources Error occurred when generate release apk

若有重新安裝 react-native 需要重做
```js
// file path: node_modules/react-native/react-gradle

doFirst {
  ...
}
/** Add doLast */
doLast {
    def moveFunc = { resSuffix ->
        File originalDir = file("$buildDir/generated/res/react/release/drawable-${resSuffix}");
        if (originalDir.exists()) {
            File destDir = file("$buildDir/../src/main/res/drawable-${resSuffix}");
            ant.move(file: originalDir, tofile: destDir);
        }
    }

    moveFunc.curry("ldpi").call()
    moveFunc.curry("mdpi").call()
    moveFunc.curry("hdpi").call()
    moveFunc.curry("xhdpi").call()
    moveFunc.curry("xxhdpi").call()
    moveFunc.curry("xxxhdpi").call()

    File originalDir = file("$buildDir/generated/res/react/release/raw");
        if (originalDir.exists()) {
            File destDir = file("$buildDir/../src/main/res/raw");
            ant.move(file: originalDir, tofile: destDir);
    }
}
```

相關 issue 連結： [https://github.com/facebook/react-native/issues/22234](https://github.com/facebook/react-native/issues/22234)