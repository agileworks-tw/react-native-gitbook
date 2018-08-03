# Drawer

## Drawer (`<Drawer>` or `<Scene drawer>`)

Can use all `prop` as listed in `Scene` as `<Drawer>`, syntatic sugar for `<Scene drawer={true}>`

| Property           | Type              | Default | Description                                                                                                |
| ------------------ | ----------------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| `drawerImage`      | `Image`           |         | Image to substitute drawer 'hamburger' icon, you have to set it together with `drawer` prop                |
| `drawerIcon`       | `React.Component` |         | Arbitrary component to be used for drawer 'hamburger' icon, you have to set it together with `drawer` prop |
| `hideDrawerButton` | `boolean`         | `false` | Boolean to show or not the drawerImage or drawerIcon                                                       |
| `drawerPosition`   | `string`          | `left`  | Determines whether the drawer is on the right or the left. Keywords accepted are `right` and `left`        |
| `drawerWidth`      | `number`          |         | The width, in pixels, of the drawer (optional)                                                             |

## 使用方法

```js
import { Drawer, Scene } from 'react-native-router-flux';
...
<Drawer>
  <Scene />
  <Scene />
  <Scene />
</Drawer>
```
