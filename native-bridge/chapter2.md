# 實作 Native module

## 模組架構說明

由於先前我們使用下列指令新增當前的專案樣板，所以展開左側的樹狀目錄之後會有兩個檔案：

```.
.
├──android     <-- 這裡
├────manifests   
├────java        
├──────com.reactlibrary
├─────────RNMyAndroidToastModule.java 
└─────────RNMyAndroidToastPackage.java
├──ios        
├──index.js  
├──package.json
└──README.md
```

![](https://i.imgur.com/K696Ygs.png)

1 `RNMyAndroidToastModule.java`

主要功能撰寫處。

2 `RNMyAndroidToastPackage.java`

這個 Native module 的主要 class，其中會包含所有要被外界存取的 modules。如果有多個 module，就要手動在 `getPackages()` 方法中加入。

### RNMyAndroidToastPackage 說明

```.
.
├──android     
├────manifests   
├────java        
├──────com.reactlibrary
├─────────RNMyAndroidToastModule.java  <-- 這裡
└─────────RNMyAndroidToastPackage.java
├──ios        
├──index.js  
├──package.json
└──README.md
```

```java
public class RNMyAndroidToastPackage implements ReactPackage {  
   @Override  
   public List<NativeModule\> createNativeModules(ReactApplicationContext reactContext) {  
  
   // 回傳 RNMyAndroidToastModule 這個 native module，可以有多個 module  
   return Arrays.<NativeModule>asList(new RNMyAndroidToastModule(reactContext));  
 }  
   // Deprecated from RN 0.47  
   public List<Class<? extends JavaScriptModule>\> createJSModules() {  
   // 舊版的建構方式 
   return Collections.emptyList();  
 }  
   @Override  
   public List<ViewManager\> createViewManagers(ReactApplicationContext reactContext) {  
   // react-native-create-library 目前不支援自動產生 UI 類 native module  
   return Collections.emptyList();  
 }}
 
```

### RNMyAndroidToastModule 說明

```.
.
├──android     
├────manifests   
├────java        
├──────com.reactlibrary
├─────────RNMyAndroidToastModule.java  
└─────────RNMyAndroidToastPackage.java  <-- 這裡
├──ios        
├──index.js  
├──package.json
└──README.md
```

```java
public class RNMyAndroidToastModule extends ReactContextBaseJavaModule {  
  
   private final ReactApplicationContext reactContext;  
  
   // 預設建構子  
   public RNMyAndroidToastModule(ReactApplicationContext reactContext) {  
   super(reactContext);  
	 
   // reactContext 是特殊的 Android Context，是當前 React Native app 的上下文物件  
   this.reactContext = reactContext;  
 }  
   // getName() 為必備方法，負責回傳此 library 名稱
   // 這裡的名稱一經產生後建議不要再修改，容易出問題
   @Override  
   public String getName() {  
   return "RNMyAndroidToast";  
 }}

```

### index.js 說明

```.
.
├──android     
├────manifests   
├────java        
├──────com.reactlibrary
├─────────RNMyAndroidToastModule.java  
└─────────RNMyAndroidToastPackage.java 
├──ios        
├──index.js	<-- 這裡
├──package.json
└──README.md
```

此檔案是整個 native module 的 JavaScript 進入點，我們可以在這裡額外針對要 export 的物件做處理，例如加上 event handler，定義 event 或 callback 發生時由哪個 method 負責。

```javascript
import { NativeModules } from  'react-native';

// 由 react native 套件中取出已經註冊的 Native module
// 這裡的名稱就是我們寫在 getName() 中回傳的名稱
const { RNMyAndroidToast } = NativeModules;

export default RNMyAndroidToast;
```