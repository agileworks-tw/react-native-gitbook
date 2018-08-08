# Props 組件的參數

> Props 是將資料從 Component 外部傳遞給 Component 內部的媒介

- 在 Component 內部透過 this.props 取得傳遞進來的 Props 資料物件
- 當 Props 資料傳遞到 Component 內部後，是不可變更的固定值 !!!

- 設計 Component 時抽象化出變動資料的 Props，方便進行重用

- JSX 中，若想要傳遞的 Props 的值是字串的話，可以直接使用雙引號，其他型別的值則需要使用 {} 來包住

```jsx
class App extends Component {
  onButtonPress = () => {
    Alert.alert('pressed');
  };
  render() {
    return (
      <View>
        <Button
          title="Press Me"
          color={'#841584'}
          onPress={this.onButtonPress}
        />
      </View>
    );
  }
}
```

## 特別提醒

- 原生組件在各個平台上支援的屬性可能不同
- 如果只填寫屬性名稱不指定值，其值為 true

## Prop 傳遞屬性資料

> #### 練習： Props Sample: MultiLine TextInput [https://snack.expo.io/@dmoon/props-sample:-multiline-textinput](https://snack.expo.io/@dmoon/props-sample:-multiline-textinput)

## 新增自定義 Component

```jsx
class Greeting extends Component {
  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}
```

```jsx
class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{ alignItems: 'center' }}>
        <Greeting name="React" />
        <Greeting name="Native" />
        <Greeting name="JavaScript" />
      </View>
    );
  }
}
```

> #### 練習： Add Custom Components: [https://snack.expo.io/@dmoon/add-custom-components](https://snack.expo.io/@dmoon/add-custom-components)

## Component 封裝

### Default Props ( prop 初始值 )

第一種寫法

```jsx
class Greeting extends Component {
  static defaultProps = {
    name: 'Nobody',
    anotherProp: ''
  };

  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}
```

第二種寫法

```jsx
class Greeting extends Component {
  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}

Greeting.defaultProps = {
  name: 'Nobody',
  anotherProp: ''
};
```

### PropType Validation ( prop 型別驗證 )

PropTypes Document: [https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)

```jsx
import PropTypes from 'prop-types';

class Greeting extends Component {
  static propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number,
    headerComponent: PropTypes.element
  };

  render() {
    return <Text>Hello {this.props.name}!</Text>;
  }
}
```

> #### 練習： Add Custom Component with defaultProps and propTypes [https://snack.expo.io/@dmoon/add-custom-component-with-defaultprops-and-proptypes](https://snack.expo.io/@dmoon/add-custom-component-with-defaultprops-and-proptypes)
