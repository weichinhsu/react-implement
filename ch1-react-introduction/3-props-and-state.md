# 1-3 props 與 state

> 本章節會沿用上一個章節建立的 my-first-project 專案。

## 1. props 屬性

在 React 中建立 Component 時，可以使用各種自定義參數設定 Component，而這些自定義參數便是 props 屬性。props 在 Component 中扮演十分重要的角色，它負責了Component 間的屬性資料的傳遞，因此如果擁有多個 Component，如何使用 props 便成為一個很重要的問題。

我們先以一個簡單的例子，來說明 Component 間屬性資料傳遞的方式，首先在App.js中，建立一個Hello元件。

```javascript
class Hello extends Component{
  render(){
    return(
      <p>Hello {this.props.title}</p>
    )
  }
}
```

**範例說明**  
第4行程式碼，撰寫一個 p 元素，並且裡面放置 this.props.title，並且由大括弧包起，表示此處會顯示由父元件所傳遞過來的 title 屬性。

接著，回到預設輸出的 App 主元件，並且呼叫上述所建立的元件。

```javascript
export default class App extends Component{
  render(){
    return(
      <div>
        <Hello title="World!"/>        
        <Hello title="React!"/>
      </div>
    )
  }
}
```

**範例說明**  
第5-6行程式碼，呼叫 Hello 元件，且定義一個名為 title 的屬性並設定屬性值。

在元件中，也可以定義多個屬性，我們接續前一個範例，設定 Hello 元件擁有三個屬性，分別為 title、name 和 id，如下所示：

```javascript
class Hello extends Component{
  render(){
    return(
      <div>
        <p>title: {this.props.title}</p>
        <p>name: {this.props.name}</p>
        <p>id: {this.props.id}</p>
      </div>
    );
  }
}
```

**範例說明**  
第5-7行程式碼，將屬性分別顯示到頁面上。

在 App 主元件中，便可以使用 this.props 設定 title、name 和 id 三個屬性值，如下所示：

```javascript
export default class App extends Component{
  render(){
    return(
      <Hello title="World" name="User" id="1654"/>
    )
  }
}
```

**範例說明**  
第4行程式碼，呼叫 Hello 元件，定義 title、name 和 id 三個屬性，並設定屬性值。

了解 props 使用方法後，必須注意一點，在 Component 中，props 是不可改變的，這句話可以理解成，父元件傳遞過來的屬性，無法在子元件中進行更動，如下所示：

```javascript
this.props.title = 'My props!'
this.props.name = 'John'
```

上述的程式碼，可以看到我們試圖更改 title 和 name 屬性的值，但這是錯誤的寫法，唯一能改變 props 的條件是操作父元件去改變子元件的 props。

但當我們一定需要改變資料時，就可以使用接下來要介紹的state來處理。

## 2. state 狀態

Component 中，除了 props 外，還有另外一種可以控制 Component 的狀態 state，這邊我們可以理解成，props 是由父元件所傳入的屬性，而 state 便是由元件自己建立的內部變數，因此 props 在 Component 中是不可修改的，但 state 是可以更改的，所以遇到需要改變的資料，或是 Component 需要設定動態的變數，讓頁面可以更為生動時，都可以透過 state 來實現。

值得注意的一點，前面提到 state 是在元件中，自行建立的內部變數，因此不同的元件內，便無法存取其他元件的 state。

### 2-1 初始 state

一般來說，使用 state 時會先設定初始狀態值，方式有兩種，第一種是使用 Comepnent 的生命週期方法 constructor，第二種是直接給定 state 值，如下所示：

```javascript
// 方式 1: 簡化寫法
state = {
  test: 0
}

// 方式 2
constructor(props){
  super(props)
  this.state = {
    test: 0
  }
}
```

**程式碼說明** 

1. 上述程式碼可以看到不管是方式 1 或是方式 2 ，都設定了一個 test state，並指定值為 0。 
2. 生命週期的用法在後面章節會詳細說明，此小節只需要了解 constructor 方法可以初始狀態值即可。

接著，可以嘗試在專案中練習 state 的使用方式，如下：

```javascript
class App extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      myState: 'My first state',
      saySomething: 'Hello World'
    }
  }

  render (){
    return (
      <div className="App">
        <p>{this.state.myState}</p>
        <p>{this.state.saySomething}</p>
      </div>
    );
  }
}

export default App;
```

### 2-1 改變 state

接下來介紹如何改變 state 的值，state 的值無法直接修改，必須透過 setState\(\) 改變才能觸發 render\(\)更新頁面，將新的狀態值顯示在畫面上。

我們將承接上一小節的範例進行說明，首先在 App 組件中，建立一個 changeText\(\)方法，如下所示：

```javascript
class App extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      myState: 'My first state',
      saySomething: 'Hello World'
    }
  }

  changeTxext = () => {
    this.setState({ saySomething: 'How are you?' })
  }

  render() {
    return (
      <div className="App">
        <p>{this.state.myState}</p>
        <p>{this.state.saySomething}</p>
        <button onClick={this.changeTxext}>Click</button>
      </div>
    );
  }
}

export default App;
```

**程式碼說明**

1. 在 changeTxext 方法中，使用 setState\(\)，改變 saySomething 的值，並將新的狀態設定為 How are you。這邊值得注意的是，setState\(\)可以個別更改狀態，因此修改了 saySomething，myState 並不會受到影響。 
2. 在render方法中，建立 button 按鈕元素，並設定 onClcik 屬性綁定 changeText\(\) 方法，表示當按下按鈕後，會觸發並執行 changeText\(\) 中的 setState\(\)，來改變 saySomething 的值。

#### 補充筆記：箭頭函式 \(Arrow Function\)

> 簡單來說，就是函式的簡短寫法

箭頭函式\(Arrow Functions\) 是在ES6 中十分常見的語法，**它可以簡短 function 程式的行數，提升整體程式的可讀性，同時也可以綁定 this 值**。

如果不使用箭頭函式，就必須在 constructor 中綁定\(bind\) this 值，如下：

```javascript
class App extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      myState: 'My first state',
      saySomething: 'Hello World'
    }
    this.changeTxext = this.changeTxext.bind(this); // 綁定 this
  }

  //不使用箭頭函式
  changeTxext() {
    this.setState({ saySomething: 'How are you?' })
  }

  render() {
    return (
      <div className="App">
        <p>{this.state.myState}</p>
        <p>{this.state.saySomething}</p>
        <button onClick={this.changeTxext}>Click</button>
      </div>
    );
  }
}
```

#### 更簡單的寫法

如果只有要更新 state，可以直接在 onClick 中加入箭頭函式，並 setState 即可。

```javascript
class App extends React.Component {
  state = {
    myState: 'My first state',
    saySomething: 'Hello World'
    }
  }

  render() {
    return (
      <div className="App">
        <p>{this.state.myState}</p>
        <p>{this.state.saySomething}</p>
        <button onClick={() => this.setState({ saySomething: 'How are you?' })}>Click</button>
      </div>
    );
  }
}
```

如果這篇文章對你有幫助，可以前往 [Github react-implement](https://github.com/weichinhsu/react-implement) 按下 Star 來支持我，我會不定期的更新教學內容。 也可以 follow 我的 Github 帳號，未來我也會繼續寫更多的網頁技術與大家分享！

