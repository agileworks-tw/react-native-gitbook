# JSX

> JSX 是 React 在使用的一種特殊 JavaScript 語法糖

- 需要翻譯成原本的 React.createElement 語法才能執行

- 能夠讓你以可讀性較高的語法來定義 React UI 結構

```jsx
// JSX
<View>
  <Button>click me</Button>
  <Image />
</View>
```

```javascript
// 透過 Babel compile 得到的 JavaScript
React.createElement(
  View,
  null,
  React.createElement(Button, null, 'click me'),
  React.createElement(Image, null)
);
```

## 語法規則

- 嚴格的標籤閉合語法

- 擁有屬性參數
- 屬性名稱改成以小駝峰式命名

```jsx
<Button title="Press Me" color={'#841584'} onPress={() => {}} />
```

## 表達式的印出顯示

> 使用 { } 語法來填入 JavaScript 表達式（一個值），其中可直接當作顯示內容印出的型別有：

### 可印出的型別

- String：直接印出
- React Element：當作子節點插入

- Number：轉成字串後直接印出

- Array：攤平成多個表達式後印出（如果 item 的值也是這些可印的型別）

- Boolean、Null、Undefined：什麼都不印，直接忽略

> ####  練習： JSX Expression Sample: [https://snack.expo.io/@dmoon/jsx-expression-demo](https://snack.expo.io/@dmoon/jsx-expression-demo)

### 條件判斷式

- JSX 中不可以直接寫 if / else，因為實際上是一個 React Element 物件結構
- 使用 && 運算子來達到 if 判斷式的效果

- 使用三元運算子來達到 if / else 判斷式的效果

#### && 運算子

```jsx
<View>{a > 100 && <Text> 超過一百分 </Text>}</View>
```

#### 三元運算子

```jsx
<View>
  {a > 100 ? <Text> 超過一百分 </Text> : <Text> 八十七分，不能再高 </Text>}
</View>
```

### 透過 function 包裝

> 將邏輯包裝在 function 中，在需要執行時調用 function

1.  先在 function 中進行判斷，回傳不同 React Element
2.  最後在 JSX 印出

#### 直接執行

```jsx
<View>
  {(() => {
    if (enable) return <Text>Enable</Text>;
    else return <Text>Disable</Text>;
  })()}
</View>
```

#### 先執行，將回傳結果存在變數中

```jsx
render() {
   const comp = getTextByEnable();
   return {
     <View>
        {comp}
     </View>
   }
}
```

> ####  練習： JSX Conditional Render Sample [https://snack.expo.io/@dmoon/jsx-conditional-render](https://snack.expo.io/@dmoon/jsx-conditional-render)

## Inline Style

- 使用 JavaScript Object 來撰寫
- Style Property：名稱改用駝峰式命名

```jsx
const styles = {
  padding: 15,
  backgroundColor: 'yellow',
}

<Button style={styles}> Press Me </Button>
```

## 註解語法

> 透過表達式與 JS 註解符號達成

```jsx
<View>
  {/* <Text> won't show </Text> */}
  <Text
  // style={{ color: 'red'}}
  >
    will show
  </Text>
</View>
```

> ####  練習： JSX Comment Sample: [https://snack.expo.io/@dmoon/jsx-comment-demo](https://snack.expo.io/@dmoon/jsx-comment-demo)

## 迭代輸出顯示內容

- 使用陣列型別的 map 函數批量迭代產生 React Element 或其他顯示內容的陣列
- 當陣列中的 item 是 React Element 時，應該要給予一個唯一的 key，以優化重繪時的 Reconciliation 效率

```jsx
<View>{numbers.map((number, key) => <Button key={key}>{number}</Button>)}</View>
```
