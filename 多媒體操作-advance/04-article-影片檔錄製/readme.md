# 影片檔錄製

## 套件

`react-native-camera` : [https://github.com/react-native-community/react-native-camera](https://github.com/react-native-community/react-native-camera)

### 安裝方法

```bash
npm install react-native-audio --save
react-native link react-native-camera
```

### 權限

錄製影片需要取得相機、麥克風、相簿等權限，因此需要到原生專案做相關設定

#### iOS

`Info.plist`

```plist
<key>NSCameraUsageDescription</key>
<string>Your message to user when the camera is accessed for the first time</string>

<!-- Include this only if you are planning to use the camera roll -->
<key>NSPhotoLibraryUsageDescription</key>
<string>Your message to user when the photo library is accessed for the first time</string>

<!-- Include this only if you are planning to use the microphone for video recording -->
<key>NSMicrophoneUsageDescription</key>
<string>Your message to user when the microphone is accessed for the first time</string>
```

#### Android

`AndroidManifest.xml`

```xml
 <uses-permission android:name="android.permission.CAMERA" />
 <uses-permission android:name="android.permission.RECORD_AUDIO"/>
 <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

### 整合

#### Android

參考以下設定，修改檔案內容

`android/gradle.properties`

```properties
android.useDeprecatedNdk=true
android.enableAapt2=false
```

`android/build.gradle`

```gradle
buildscript {
    repositories {
        google()
        maven {
            url 'https://maven.google.com/'
            name 'Google'
        }
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.0'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        mavenLocal()
        jcenter()
        maven {
            url 'https://maven.google.com/'
            name 'Google'
        }
        maven { url "https://jitpack.io" }
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
    }
}

subprojects {
    project.configurations.all {
        resolutionStrategy.eachDependency { details ->
            if (details.requested.group == 'com.android.support'
              && !details.requested.name.contains('multidex') ) {
                details.useVersion "26.0.1"
            }
        }
    }
    
    afterEvaluate { 
        project -> if (project.hasProperty("android")) { 
            android { 
                compileSdkVersion 26 
                buildToolsVersion '26.0.1' 
            } 
        } 
    } 
}
```

`android/app/build.gradle`

```gradle
android {
    compileSdkVersion 26
    buildToolsVersion "26.0.1"

    defaultConfig {
        applicationId "appName"
        minSdkVersion 16
        targetSdkVersion 22
        versionCode 1
        versionName "1.0"
        ndk {
            abiFilters "armeabi-v7a", "x86"
        }
    }

...

dependencies {
    implementation project(':react-native-camera')
    ...
    implementation fileTree(dir: "libs", include: ["*.jar"])
    implementation 'com.android.support:appcompat-v7:26.0.1'
    implementation "com.facebook.react:react-native:+"  // From node_modules
}
```

`android/gradle/gradle-wrapper.properties`

```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip
```

#### 整合問題

若 Android 打包時出現

```
A problem occurred configuring project ':react-native-sound'.
      > The SDK Build Tools revision (23.0.1) is too low for project ':react-native-sound'.Minimum required is 25.0.0
```

找到檔案 `node_modules/react-native-sound/android/build.gradle`
修改 `compileSdkVersion` 和 `buildToolsVersion` 參數如下

```gradle
  compileSdkVersion 26
  buildToolsVersion "26.0.3"
```

## 使用方式

#### 錄影

使用 ref 調用 RNCamera 的 `recordAsync` function 進行相機錄製，並會在停止錄影後回傳影片資訊

```js
const recordVideo = await this.camera.recordAsync();
```

#### 停止錄影

使用 ref 調用 RNCamera 的 `stopRecording`  停止錄製

```js
this.camera.stopRecording();
```