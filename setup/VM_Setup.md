# VM 使用教學

## 取得 VM 相關檔案

跟講師領取隨身碟或透過網路下載

## 前置準備

- 安裝 Virtual Box

- 安裝 Genymotion

- 將虛擬機檔案 `ReactNative.ova` 匯入 VirtualBox

## VM 環境設定

[環境使用教學影片](https://youtu.be/2m7YyRycMhE)
**請依照順序操作**

1.  開啟 Genymotion
2.  開啟 Genymotion 當中的 Android 虛擬機 **Custom Phone - 7.1.0 - API 25 - 768x1280**，等待開機完成
3.  在 `本機` 電腦執行命令提示字元執行指令

```bash
$ adb devices
$ adb tcpip 5556
```

4.  開啟 VirtualBox 當中的 ReactNative 虛擬機
5.  ReactNative 虛擬機出現 login 字樣，開啟網頁 http://localhost:9083/ide.html
6.  到 `ReactNative 虛擬機網頁當中的 terminal` 視窗輸入指令

```bash
$ adb connect $ip:5556
/* $ip 請自行替換為 adb devices 回傳的 Android 虛擬機 IP 例如: adb connect 192.168.57.101:5556 */
$ adb devices
/* 測試是否有連上 */
$ adb shell am start -a android.settings.SETTINGS
```

## 常見問題

[常見問題](http://bbs.reactnative.cn/topic/130/%E6%96%B0%E6%89%8B%E6%8F%90%E9%97%AE%E5%89%8D%E5%85%88%E6%9D%A5%E8%BF%99%E9%87%8C%E7%9C%8B%E7%9C%8B-react-native%E7%9A%84%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)

## 延伸閱讀

- 官方文件 Android 開發環境 - for Mac: [http://facebook.github.io/react-native/releases/0.44/docs/getting-started.html#android-development-environment](http://facebook.github.io/react-native/releases/0.44/docs/getting-started.html#android-development-environment)
- 官方文件 Android 開發環境 - for Windows: [http://facebook.github.io/react-native/releases/0.44/docs/getting-started.html#android-development-environment](http://facebook.github.io/react-native/releases/0.44/docs/getting-started.html#android-development-environment)
- 簡中環境教學: [http://reactnative.cn/docs/0.47/getting-started.html](http://reactnative.cn/docs/0.47/getting-started.html)
