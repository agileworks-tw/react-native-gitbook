# 音檔錄製

## 套件

`react-native-audio` :  [https://github.com/jsierles/react-native-audio](https://github.com/jsierles/react-native-audio)

### 安裝方法

```bash
npm install react-native-audio --save
react-native link react-native-audio
```

### 權限

要在手機錄製聲音需要先取得麥克風權限，因此需要到原生專案新增麥克風的權限設定

#### iOS

`Info.plist`

```plist
<key>NSMicrophoneUsageDescription</key>
<string>This sample uses the microphone to record your speech and convert it to text.</string>
```

#### Android

`AndroidManifest.xml`

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
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

iOS: Build input file double-conversion cannot be found


```bash
cd node_modules/react-native/scripts && ./ios-install-third-party.sh && cd ../../../
cd node_modules/react-native/third-party/glog-0.3.4/ && ../../scripts/ios-configure-glog.sh && cd ../../../../
```

## 使用方式

這個套件不是 Component，只提供封裝的方法調用

使用範例

```js
import { AudioRecorder, AudioUtils } from 'react-native-audio';
let audioPath = AudioUtils.DocumentDirectoryPath + '/test.aac';

// 取得權限
AudioRecorder.requestAuthorization().then((isAuthorised) => {

});

// 錄音參數設定
AudioRecorder.prepareRecordingAtPath(audioPath, {
  SampleRate: 22050,
  Channels: 1,
  AudioQuality: "Low",
  AudioEncoding: "aac"
});

// 開始錄製
AudioRecorder.startRecording();

// 停止錄製(結束)
AudioRecorder.stopRecording();
```

