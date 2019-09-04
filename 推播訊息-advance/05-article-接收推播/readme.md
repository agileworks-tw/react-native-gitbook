# 接收推播

## 使用方法

### hasPermission

取得當前是否有 messaging 權限

```js
const enabled = await firebase.messaging().hasPermission();
if (enabled) {
    // user has permissions
} else {
    // user doesn't have permission
}
```

### Request Permissions

請求 messaging 權限

```js
try {
    await firebase.messaging().requestPermission();
    // User has authorised
} catch (error) {
    // User has rejected permissions
}
```

### onNotification

App 在前景收到訊息時會調用此事件

```js
import type { Notification } from 'react-native-firebase';

componentDidMount() {
    this.notificationListener = firebase.notifications().onNotification((notification: Notification) => {
        // Process your notification as required
    });
}

componentWillUnmount() {
    this.notificationListener();
}
```

### NotificationOpen

開起通知時的監聽事件

```js
import type { Notification, NotificationOpen } from 'react-native-firebase';

componentDidMount() {
    this.notificationOpenedListener = firebase.notifications().onNotificationOpened((notificationOpen: NotificationOpen) => {
        // Get the action triggered by the notification being opened
        const action = notificationOpen.action;
        // Get information about the notification that was opened
        const notification: Notification = notificationOpen.notification;
    });
}

componentWillUnmount() {
    this.notificationOpenedListener();
}
```

### Notification 事件

|         | App in foreground | App in background                                            | App closed             |
| ------- | ----------------- | ------------------------------------------------------------ | ---------------------- |
| Android | onNotification    | onNotificationOpened                                         | getInitialNotification |
| iOS     | onNotification    | `onNotificationDisplayed`triggered if `content_available ` set to `true` , `onNotificationOpened`triggered if the notification is tapped | getInitialNotification |

