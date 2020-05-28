# 1-2 Component 元件

在 React 中，提供一個非常重要的 Component 元件機制，它可以讓開發者可以自行定義元件，讓在開發的過程中，若遇到需要重複使用的元件，可以將一樣的部分自行定義成一個元件，當需要用到時直接呼叫使用即可，除了可以減少程式的複雜度，也可以避免程式中有過多相同的邏輯語法。

> 本章節會沿用上一個章節建立的 my-first-project 專案。

## 1. 自訂元件

在自定義元件中，可以包含多種內建的元件，舉例來說，當一個頁面是讓使用者填寫資料，想必會出現許多的 Input 輸入框，而每個輸入框又都需要搭配文字說明，因此這時候就很適合使用自訂元件，將輸入框元件與文字元件組合成一個自訂元件，當需要用到時再呼叫此自訂元件即可，而這就可以縮減頁面上的程式行數，讓程式看起來更易懂。

React 自訂元件的方式可以分為兩種 `Function Component` 與 `Class Component`，並透過 `Html` 標籤來組成，以下分別介紹使用方式。

### 1-1 Function Component

最簡單的建立 Component 的方式就是透過 function 來建立，如下程式碼，是我們在前一章節建立 my-first-project 專案後，預設的頁面元件。

```javascript
// 路徑 : src/App.js
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  )
}
```

**程式碼說明**  
透過 function 來建立一個名為 App 的元件，這邊需要注意，在方法中，我們需要將定義的內容回傳\(return\)，而定義的內容也可以稱為 React Element。

接下來，我們來試著定義一個 Component，如下：

```javascript
// 路徑 : src/App.js
function Welcome() {
  return (
    <div className="App">
      <h1>Hello React</h1>
      <h2>My name is Winnie.</h2>
    </div>
  )
}

export default Welcome
```

**程式碼說明**  
定義一個 Welcome 元件，修改完後，記得在最後面的 export default 要將元件改為輸出 Welcome。

### 1-2 Class Component

而在建立自訂元件的時候，一個非常重要的地方是，**自訂元件需要 extends 繼承 React Component**，這表示之後在此元件中，便可以使用 React 提供的 `State` 狀態以及`生命週期`，這讓元件可以更容易的進行不同的操作。

而本小節將會教導讀者，如何設計一個簡單且實用的自訂元件，其中 State 以及生命週期的使用方式，會分別在往後的章節介紹。

首先，建立一個 Welcome 元件，並繼承 React.Component，如下所示：

```javascript
// 路徑 : src/App.js
class Welcome extends React.Component {
  render() {
    return <div>
      <h1>Hello React</h1>
      <h2>My name is Winnie.</h2>
    </div>
  }
}

export default Welcome
```

**程式碼說明**  
上述程式碼可以看到，render 是在生命週期中用來渲染頁面的方法，透過 render 將要渲染的頁面回傳（return）到畫面上顯示，詳細的生命週期用法將會在後面章節介紹，現在只要了解其代表的意思即可。

## 2. 使用自訂元件

接下來，在同個檔案中再新增一個主要元件，如下：

```javascript
// 路徑 : src/App.js
class Welcome extends React.Component {
  render() {
    return <div>
      <h1>Hello React</h1>
      <h2>My name is Winnie.</h2>
    </div>
  }
}

class Main extends React.Component {
  render() {
    return <div>
      <Welcome/>
      <Welcome/>
      <Welcome/>
    </div>
  }
}

export default Main
```

**程式碼說明**  
1. 在 Main 元件中，可以重複呼叫 Welcome 元件，如此一來，就可以縮減頁面上的程式行數，讓程式更好閱讀。 
2. 記得在最後面的 export default 要將元件改為輸出 Main。

---

如果這篇文章對你有幫助，可以前往 [Github react-implement](https://github.com/weichinhsu/react-implement) 按下 Star 來支持我，我會不定期的更新教學內容。
也可以 follow 我的 Github 帳號，未來我也會繼續寫更多的網頁技術與大家分享！