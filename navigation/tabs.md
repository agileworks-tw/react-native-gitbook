# Tabs

## Tabs (`<Tabs>` or `<Scene tabs>`)


| Property                  | Type              | Default | Description                                                                     |
| ------------------------- | ----------------- | ------- | ------------------------------------------------------------------------------- |
| `wrap`                    | `boolean`         | `true`  | Wrap each scene with own navbar automatically (if it is not another container). |
| `activeBackgroundColor`   | `string`          |         | Specifies the active background color for the tab in focus                      |
| `activeTintColor`         | `string`          |         | Specifies the active tint color for tabbar icons                                |
| `inactiveBackgroundColor` | `string`          |         | Specifies the inactive background color for the tabs not in focus               |
| `inactiveTintColor`       | `string`          |         | Specifies the inactive tint color for tabbar icons                              |
| `labelStyle`              | `object`          |         | Overrides the styles for the tab label                                          |
| `lazy`                    | `boolean`         | `false` | Won't render/mount the tab scene until the tab is active                        |
| `tabBarComponent`         | `React.Component` |         | React component to render custom tab bar                                        |
| `tabBarPosition`          | `string`          |         | Specifies tabbar position. Defaults to `bottom` on iOS and `top` on Android.    |
| `tabBarStyle`             | `object`          |         | Override the tabbar styles                                                      |
| `tabStyle`                | `object`          |         | Override the style for an individual tab of the tabbar                          |
| `showLabel`               | `boolean`         | `true`  | Boolean to show or not the tabbar icons labels                                  |
| `swipeEnabled`            | `boolean`         | `false` | Enable or disable swiping tabs.                                                 |
| `animationEnabled`        | `boolean`         | `true`  | Enable or disable tab swipe animation.                                          |
| `tabBarOnPress`           | `function`        |         | Custom tab bar icon press.                                                      |
| `backToInitial`           | `boolean`         | `false` | Back to initial screen on focused tab if tab icon was tapped.                   |
| `upperCaseLabel`          | `boolean`         | `true`  | Whether to make label uppercase, default is true.                               |

## Tab Scene (child `<Scene>` within `Tabs`)


| Property      | Type        | Default     | Description                                     |
| ------------- | ----------- | ----------- | ----------------------------------------------- |
| `icon`        | `component` | `undefined` | a React Native component to place as a tab icon |
| `tabBarLabel` | `string`    |             | The string to override a tab label              |

## 使用方法

```js
import { Tabs, Tab } from 'react-native-router-flux';
...
<Tabs>
  <Tab icon={TabIcon} title="tab1"/>
  <Tab icon={TabIcon} title="tab2"/>
  <Tab icon={TabIcon} title="tab3"/>
</Tabs>
```

`TabIcon`

```js
const TabIcon = props => 
  <Text style={{ color: props.focused ? 'red' : 'black' }}>
    {props.title}
  </Text>;
```
