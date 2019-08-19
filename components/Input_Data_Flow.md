# Input Data Flow

> 原生的 HTML `<input />` or RN `<TextInput />`
> 元素是自帶資料狀態的

在 React 中，有兩種處理方式

- Uncontrolled：依照原來的自帶資料狀態模式

- Controlled：使用單向資料流的模式，將資料存於獨立地點，使其可被 React 控制，並將資料綁定到 UI

## Uncontrolled Input

> input 本身自己管理資料狀態，不與資料來源綁定

- 使用 defaultValue 來設定預設值

- 這種做法代表你不能夠透過修改資料來源來隨意控制現在 Input 的值，也沒有一個集中地點可以取得目前 Input 的值

```jsx
class UncontrolledInputExample extends Component {
  onChangeText = text => {
    this.setState({ text });
  };

  render() {
    return (
        <TextInput onChangeText={this.onChangeText} />
    );
  }
}
```

> #### 範例： Uncontrolled Input: [https://snack.expo.io/@dmoon/uncontrolled-input](https://snack.expo.io/@dmoon/uncontrolled-input)

## Controlled Input

> Input 自己本身不存放資料，也不能隨意改變自己顯示的值，與指定的資料來源綁定

- 使用 value 來綁定資料來源
- 使用 onChangeText 指定接收資料的函數，並且在該函數中更新資料來源，使新資料再透過 value 更新 input

```jsx
class ControlledInputExample extends Component {
  state = {
    inputText: 'default'
  };

  handleInputChange = value => {
    this.setState({
      inputText: value
    });
  };

  render() {
    return (
      <TextInput
        type="text"
        value={this.state.inputText}
        onChangeText={this.handleInputChange}
      />
    );
  }
}
```

> #### 範例： Controlled Input: [https://snack.expo.io/@dmoon/controlled-input](https://snack.expo.io/@dmoon/controlled-input)

### 小試身手： BMI 計算機

參考範例: [https://snack.expo.io/@dmoon/bmi](https://snack.expo.io/@dmoon/bmi)
