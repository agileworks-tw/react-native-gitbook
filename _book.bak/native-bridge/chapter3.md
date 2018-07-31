# Linking Projects

## Link native module 以及 React Native project

已經完成的 Native module 需要透過 `link` 後才能在 Reacyt Native 專案中使用。這個過程一般來說有三種方式：

1.  將套件發佈到 npm，然後使用 `npm install {套件名稱}` 安裝。
2.  使用在 `package.json` 指定相對路徑的方式，透過 `npm install` 安裝。
3.  使用 [yarn link](https://yarnpkg.com/lang/zh-hans/docs/cli/link/) 指令綁定開發中的 native module 與 RN 專案。

如果你想要讓任何人都能使用你的 module，那第一種方式會是整個 native module 製作完成後需要處理的部分；而如果你是多人一起開發 native module 與 RN 專案
，那寫入你的 module 的路徑到 `package.json` 就會是必備的。

最後在本教學中，會採用最後一種方式進行操作。完成這個步驟之後，還需要執行 `react-native link` 指令來自動將對應的 module package 連結起來。 
