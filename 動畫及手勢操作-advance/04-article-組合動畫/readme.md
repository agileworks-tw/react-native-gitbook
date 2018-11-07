# 組合動畫

使用下列的 Animated 函數組合多個動畫，實現同時播放或依序播放的效果。

- parallel (同時執行)
- sequence (依序執行動畫，結束才開始下一個)
- stagger  (依序延遲一段時間調用下一個動畫開始，不會等上一個動畫結束才開始計算延遲)
  - Stagger Animation Sample: [https://i.imgur.com/2iP68An.gifv](https://i.imgur.com/2iP68An.gifv)
- delay    (延遲)

範例

```js
// 依序執行陣列中的動畫
Animated.sequence([
  // decay, then spring to start and twirl
  Animated.decay(position, {
    // coast to a stop
    velocity: { x: gestureState.vx, y: gestureState.vy }, // velocity from gesture release
    deceleration: 0.997
  }),
  // 同時執行陣列中的動畫
  Animated.parallel([
    // after decay, in parallel:
    Animated.spring(position, {
      toValue: { x: 0, y: 0 } // return to start
    }),
    Animated.timing(twirl, {
      // and twirl
      toValue: 360
    })
  ])
]).start(); // 開始依序執行動畫
```