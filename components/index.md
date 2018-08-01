# 常用組件

## 組件使用方式

參考 [官方文件: <https://facebook.github.io/react-native/docs/getting-started>](https://facebook.github.io/react-native/docs/getting-started) 左側的 Components 列表，可以找到各組件提供的 props 、methods 與使用方式

## Image

顯示圖片，可使用本地圖片檔案或是圖片 url

props

- style

  要記得設定`寬度`、`高度`!!!

- source

  `require('圖片檔案路徑')` 或是 `{ url: '圖片網址' }`

[使用範例: <https://snack.expo.io/@dmoon/image-sample>](https://snack.expo.io/@dmoon/image-sample)

## TouchableOpacity

含有 onPress prop 的可按視圖(View)，可用來包裝想要加上按扭事件的組件

props

- onPress

## ScrollView

[使用範例: <https://snack.expo.io/@dmoon/scrollview-sample>](https://snack.expo.io/@dmoon/scrollview-sample)

## FlatList

顯示項目列表的組件，包含列表相關的 prop 功能 (無限捲動、下拉更新......)

props

- data
- renderItem

[使用範例: <https://snack.expo.io/@dmoon/flatlist-sample>](https://snack.expo.io/@dmoon/flatlist-sample)
