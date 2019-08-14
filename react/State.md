# State

> State 是 Component 內部的可變資料的存放載體

- 透過 this.state 取得目前 Component 個體的 State 資料物件
- 不能直接修改 state， 必須使用 this.setState 函數來更新 state 物件
  - 調用 setState 修改資料後，該 Component 以及其包含的所有子孫 Component 都會跟著自動發起重繪，以更新 Virtual DOM Tree
  - setState 方法就是 Reconciliation 流程以及 Virtual DOM 重繪的發起者，使資料變更、引發重繪，一直到最後反應出實際 DOM 的更新結果

> #### 練習： State Sample [https://snack.expo.io/@dmoon/state-sample](https://snack.expo.io/@dmoon/state-sample)

## setState Sample

```jsx
class App extends React.Component {
  state = {
    // 初始化 state 內容
    text: 'hello'
  };

  handleButton = () => {
    /* 新手常犯的錯誤 */
    this.state.text = 'hello React';

    /* 正確寫法 */
    this.setState({ text: 'hello React' });
  };

  render() {
    return (
      <View>
        <Text>{this.state.text}</Text>
        <Button title="Press Me" onPress={this.handleButton} />
      </View>
    );
  }
}
```

> #### 練習： setState Sample: [https://snack.expo.io/@dmoon/setstate-sample](https://snack.expo.io/@dmoon/setstate-sample)

### Async setState Sample

> setState 是非同步的
> 因此需要考慮非同步可能會發生的狀況
> 像是更新時如果需要從舊的資料計算出新的資料，就要特別注意

```jsx
class Counter extends React.Component {
  state = {
    count: 0
  };

  handleIncrement = () => {
    /* 錯誤示範　*/
    this.setState({
      count: this.state.count + 1
    });

    /* 正確寫法 */
    this.setState(prevState => ({
      count: prevState.count + 1
    }));
  };

  render() {
    return (
      <View>
        <Text>{this.state.count}</Text>
        <Button title="Add" onPress={this.handleIncrement} />
      </View>
    );
  }
}
```

> #### 練習： Counter Sample: [https://snack.expo.io/@dmoon/setstate-sample:-counter](https://snack.expo.io/@dmoon/setstate-sample:-counter)

## State 提升

在 App 開發過程中，總有些資料是需要同時分享給多個組件，讓這些組件在資料發生變化時，能夠去反應資料的變動更新畫面，這個時候我們會盡量將需要共用的 state 提升到共用組件們的共同父組件來管理，再透過 prop 將資料傳入需要的組件中。

```js
export default class LotsOfGreetings extends Component {
  state = {
    name: null
  }

  onChangeText = (text) => {
    this.setState({
      name: text
    })
  }

  render() {
    return (
      <View style={{ alignItems: 'center' }}>
        <TextInput placeHolder="Name" onChangeText={this.onChangeText} style={styles.textInput}/>
        <Greeting name={this.state.name} />
        <Greeting greetingWord="Welcome" name={this.state.name} />
        <Greeting greetingWord="Hola" name={this.state.name} />
        <Greeting greetingWord="Bonjour" name={this.state.name} />
      </View>
    );
  }
}
```

> #### 範例： [https://snack.expo.io/@dmoon/lifting-state](https://snack.expo.io/@dmoon/lifting-state)