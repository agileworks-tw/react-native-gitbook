# Camera 相機和取得相簿圖片

整合系統的相機與取用本地相簿圖片

## 套件 react-native-image-picker

react-native-image-picker [https://github.com/react-community/react-native-image-picker](https://github.com/react-community/react-native-image-picker)

## 整合

```bash
yarn add react-native-image-picker
react-native link react-native-image-picker
```

## 使用方式

### 選擇圖片

```js
import ImagePicker from "react-native-image-picker";

const options = {
  title: "Select Avatar",
  customButtons: [{ name: "fb", title: "Choose Photo from Facebook" }],
  storageOptions: {
    skipBackup: true,
    path: "images"
  }
};

/**
 * The first arg is the options object for customization (it can also be null or omitted for default options),
 * The second arg is the callback which sends object: response (more info in the API Reference)
 */
// 調用 Alert 詢問視窗
ImagePicker.showImagePicker(options, response => {
  console.log("Response = ", response);

  if (response.didCancel) {
    console.log("User cancelled image picker");
  } else if (response.error) {
    console.log("ImagePicker Error: ", response.error);
  } else if (response.customButton) {
    console.log("User tapped custom button: ", response.customButton);
  } else {
    // You can also display the image using data:
    // const source = { uri: 'data:image/jpeg;base64,' + response.data };

    // 成功取得圖片資訊，更新到 state 中
    const source = { uri: response.uri };
    this.setState({
      avatarSource: source
    });
  }
});
```

### 使用取得的圖片資訊

```xml
<Image source={this.state.avatarSource} style={styles.uploadAvatar} />
```

### 直接開啟相機或  相簿

```js
// Launch Camera:
ImagePicker.launchCamera(options, response => {
  // Same code as in above section!
});

// Open Image Library:
ImagePicker.launchImageLibrary(options, response => {
  // Same code as in above section!
});
```
