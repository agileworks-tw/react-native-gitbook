# 常用組件

## 組件使用方式

參考 官方文件: [https://facebook.github.io/react-native/docs/getting-started](https://facebook.github.io/react-native/docs/getting-started) 左側的 Components 列表，可以找到各組件提供的 props 、methods 與使用方式

## Image

顯示圖片的元件，可使用本地圖片檔案或是圖片 url 作為圖片來源

props

- style

  要記得設定`寬度`、`高度`!!!

- source

  `require('圖片檔案路徑')` 或是 `{ url: '圖片網址' }`

```jsx
export default class DisplayAnImage extends Component {
  render() {
    return (
      <View>
        <Image
          style={{width: 50, height: 50}}
          source={require('@expo/snack-static/react-native-logo.png')}
        />
        <Image
          style={{width: 50, height: 50}}
          source={{uri: 'https://facebook.github.io/react-native/img/tiny_logo.png'}}
        />
      </View>
    );
}
```

使用範例: [https://snack.expo.io/@dmoon/image-sample](https://snack.expo.io/@dmoon/image-sample)

## TouchableOpacity

含有 onPress prop 的可按視圖元件(View)，可以用來包裝想要加上按扭事件的組件

props

- onPress

```jsx
<TouchableOpacity onPress={this._onPressButton}>
  <Image
    style={styles.button}
    source={require('./myButton.png')}
  />
</TouchableOpacity>
```

## ScrollView

ScrollView 是可以捲動的視圖元件，在子元件高度高於裝置高度時，可以進行捲動。

```jsx
<ScrollView>
  {/* content */}
</ScrollView>
```

使用範例: [https://snack.expo.io/@dmoon/scrollview-sample](https://snack.expo.io/@dmoon/scrollview-sample)

## FlatList

顯示項目列表的組件，包含列表相關的 prop 功能 (無限捲動、下拉更新......)

props

- data
- renderItem
- onEndReached (列表捲動到底部時觸發)
- onRefresh (下拉更新)

```jsx
<FlatList
  data={[{key: 'a'}, {key: 'b'}]}
  renderItem={({item}) => <Text>{item.key}</Text>}
/>
```

使用範例: [https://snack.expo.io/@dmoon/flatlist-sample](https://snack.expo.io/@dmoon/flatlist-sample)
