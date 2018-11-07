# 音檔播放

## 套件

`react-native-sound` :  [https://github.com/zmxv/react-native-sound](https://github.com/zmxv/react-native-sound)

## 安裝方法

```bash
npm install react-native-sound --save
react-native link react-native-sound
```


## 使用方式

```js
import Sound from 'react-native-sound';

// 載入音檔，產生音樂實體
const whoosh = new Sound('whoosh.mp3', Sound.MAIN_BUNDLE, (error) => {
  if (error) {
    console.log('failed to load the sound', error);
    return;
  }
  // loaded successfully
  console.log('duration in seconds: ' + whoosh.getDuration() + 'number of channels: ' + whoosh.getNumberOfChannels());
});

//　播放音樂
whoosh.play((success) => {
  if (success) {
    console.log('successfully finished playing');
  } else {
    console.log('playback failed due to audio decoding errors');
    // reset the player to its uninitialized state (android only)
    // this is the only option to recover after an error occured and use the player again
    whoosh.reset();
  }
});
```

