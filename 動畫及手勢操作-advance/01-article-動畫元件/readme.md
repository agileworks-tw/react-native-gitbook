# 動畫元件

React Native 中想要讓元件實現動畫效果，首先必須要先將元件透過 `Animated` API 進行動畫化的封裝，有了動畫功能支援後，再對元件進行樣式及動畫的配置。

## Animated

Animated 是 react-native library 內建的 API，封裝了 View, Text, Image, ScrollVew 四個可以設定動畫的元件，可以直接使用。

```js
import { Animated } from 'react-native';
...
  render() {
    return <Animated.View />
  }
...
```

如果你希望在其他元件上使用動畫，可以透過 `Animated.createAnimatedComponent()` 封裝客製化的元件，使其擁有動畫校果。

```js
const AnimatedCustomComponent = Animated.createAnimatedComponent(CustomComponent);
```