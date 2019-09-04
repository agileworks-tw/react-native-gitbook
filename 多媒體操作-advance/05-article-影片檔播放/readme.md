# 影片檔播放

## 套件

`react-native-video` :  [https://github.com/react-native-community/react-native-video](https://github.com/react-native-community/react-native-video)

## 安裝方法

```bash
yarn add react-native-video
react-native link react-native-video
```

## 使用方式

```xml
import Video from 'react-native-video';

<Video source={{uri: "video-path"}}   // Can be a URL or a local file.
       ref={(ref) => {
         this.player = ref
       }}                                      // Store reference
       onBuffer={this.onBuffer}                // Callback when remote video is buffering
       onError={this.videoError}               // Callback when video cannot be loaded
/>
```

