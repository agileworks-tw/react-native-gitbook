# Drawer

## Drawer (`<Drawer>` or `<Scene drawer>`)

| Property           | Type              | Default | Description                                                                                                |
| ------------------ | ----------------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| `drawerImage`      | `Image`           |         | Image to substitute drawer 'hamburger' icon, you have to set it together with `drawer` prop                |
| `drawerIcon`       | `React.Component` |         | Arbitrary component to be used for drawer 'hamburger' icon, you have to set it together with `drawer` prop |
| `hideDrawerButton` | `boolean`         | `false` | Boolean to show or not the drawerImage or drawerIcon                                                       |
| `drawerPosition`   | `string`          | `left`  | Determines whether the drawer is on the right or the left. Keywords accepted are `right` and `left`        |
| `drawerWidth`      | `number`          |         | The width, in pixels, of the drawer (optional)                                                             |
| `contentComponent`     | `React.Component` |  | Component used to render the content of the drawer (e.g. navigation items). |

## 使用方法

```js
import { Drawer, Scene } from 'react-native-router-flux';
...
<Drawer drawerIcon={DrawerIcon} contentComponent={DrawerContent}>
  <Scene />
  <Scene />
  <Scene />
</Drawer>
```
