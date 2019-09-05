# 2. 原生專案編譯

## android

### 1. Generating a signing key

`my-release-key`, `my-key-alias` 可以換成專案 App 相關名稱

```bash
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

產生的 keystore 檔案需放置到 `/android/app/`

### 2. Setting up gradle variables

編輯 `~/.gradle/gradle.properties`，加入下面幾個變數  
變數名稱中的 MYAPP 可換成專案 App 名稱  
變數的值則依照上一個指令執行時給的相關參數設定

```text
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```

### 3. Adding signing config to your app's gradle config

編輯 `android/app/build.gradle`

```gradle
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```

### 4. Generating the release APK

產生 release apk 指令

```bash
# 專案目錄下
cd android && ./gradlew assembleRelease
```

參考文件：[https://facebook.github.io/react-native/docs/signed-apk-android](https://facebook.github.io/react-native/docs/signed-apk-android)
