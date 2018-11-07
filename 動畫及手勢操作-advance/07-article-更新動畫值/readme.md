# 更新動畫值

將捲動或是拖拉、滑動等操作事件與動畫值綁定，隨著手勢的追蹤改變動畫數值。

更新有三種方式

- 透過動畫函數進行更新

  > 例如前面範例的 Animated.timing 函數，使用 toValue 設定動畫的終點值，以 easing 方式將動畫值更新到終點直結束。

- 直接賦值更新

- 綁定事件更新

## 動畫值運算

在介紹更新方法之前，我們可能需要先對動畫值進行運算，得出想要的值才進行更新，由於動畫值不是一般的數字，需要使用 Animated API 中的運算函數進行，透過這些函數才能將兩個動畫值合成新的動畫值。

### 動畫值的運算函數

- Animated.add(a, b)

- Animated.subtract(a, b)

- Animated.divide(a, b)

- Animated.modulo(a, modulus)

- Animated.multiply(a, b)

## 更新方法

### 直接賦值更新 setValue

透過 Animated.Value 或 Animated.ValueXY 產生的動畫值都有 `setValue` 函數可以進行賦值更新

```js
// initial value
state = {
  opacity: new Animated.Value(0),
  position: new Animated.ValueXY({ x: 0, y: 0 })
}
...
// update value
this.state.opacity.setValue({ x: 5, y: 0 })
// or
this.state.position.x.setValue(5);
this.state.position.y.setValue(0);
```

### 事件綁定更新

#### 捲動事件綁定

```js
 onScroll={Animated.event(
   // 將動畫值變數 scrollX 更新為 e.nativeEvent.contentOffset.x
   [{ nativeEvent: {
        contentOffset: {
          x: scrollX
        }
      }
    }]
 )}
```

#### 滑動事件綁定

```js
onPanResponderMove={Animated.event(
  [null, // ignore the native event
  // extract dx and dy from gestureState
  // like 'pan.x = gestureState.dx, pan.y = gestureState.dy'
  // 將動畫向量值變數 pan 更新為 (dx, dy)
  {dx: pan.x, dy: pan.y}
])}
```
