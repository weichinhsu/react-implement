# 1-4 生命週期

> 本章節會沿用上一個章節建立的 my-first-project 專案。

開始撰寫 React 之前，我們必須先了解頁面運作的流程，也就是 Component 的生命週期，在撰寫頁面時，才可以清楚的了解整個程式運作，並且快速上手。

首先，在下圖可以看到，React 提供許多不同的生命週期函式，且每個函式都有不同的用途，讓開發者可以依照需求，呼叫適合的方法，下面會一一跟讀者詳細介紹生命週期函式的用法。

![lifecycle](https://github.com/weichinhsu/react-implement/blob/master/images/ch1/lifecycle.PNG?raw=true)

[Reference : react-lifecycle-methods-diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

一般而言，生命週期主要分為Mounting、Updating及Unmounting，分別為頁面載入、頁面組件更新以及離開頁面，三種不同的狀態，而在這些狀態下，都會有不同的函式和使用方法，如下所示： 
1. Mounting：組件渲染階段，在這個階段完成了組件的載入和初始化。 
2. Updating：組件運行和改變階段，這個階段組件可以處理屬性\(props\)和狀態\(state\)改變，並重新渲染頁面組件。 
3. Unmounting：組件結束階段，離開頁面組件即將被移除時，便會進入此階段。

## 1. Mounting

### constructor\(props\)

constructor 主要是用來**初始化 state**，設定方式有兩種，都會在 Component 被載入頁面前呼叫，並初始化所設定的 state，如下所示：

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
2. 方式 2 實作 constructor 時，必須呼叫 super\(props\)，否則用到 this.props 時，會發生 undefined 的錯誤。 
3. 請注意，不可以在 constructor 中呼叫 setState\(\) 方法，並且當頁面上不會使用到 state 以及 props 時，可以不用實作 constructor。

super\(props\) 超詳細解說推薦：[為什麼我們要寫 super\(props\) ？](https://overreacted.io/zh-hant/why-do-we-write-super-props/)

### static getDerivedStateFromProps\(nextProps, prevState\)

組件開始載入（render）前被調用，以及每次父組件 props 更動時，也會調用此方法。此方法接收兩個參數，第一個為要更新的 props，第二個則為舊的 state 值。

此方法通常用在，子組件 state 會根據父組件的 props 改變，且當父組件 props 更新時，便可在此更新 state，但父組件有可能在沒有更新 props 的情況下，重新 render 此組件，因此子組件中，便可透過此方法，比較 nextProps\(新的 props\) 和 prevState\(舊的 state\) 有無差異，若無差異，便回傳 null 表示不更新。如下所示：

```javascript
static getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.title != prevState.title) {
    return {
      title: nextProps.title 
    };
  }
  return null;
}
```

### render\(\)

在 Component 中必須實作的方法，當每次 props 或 state 被改變時，就會調用 render\(\)，重新渲染頁面。而在 render\(\) 中，為了要讓其保持乾淨易懂，規定 render\(\) 中不能使用 setState\(\)，因為在渲染頁面的當下，只會執行一次 render\(\)，若是在這邊呼叫 setState\(\)，便會重複調用 render\(\)，導致頁面上出現錯誤。

render\(\)寫法如下所示：

```javascript
render(){
  return (
    <Text>Hello World</Text>
  )
}
```

### componentDidMount\(\)

在組件載入到頁面上後調用，DOM 節點的初始化也在此進行，而這個函式在整個生命週期中只被調用一次。當調用此函式後，頁面程式便會進入穩定的運行狀態，並開始等待其它頁面事件觸發。此方法通常用在取得資料，例如 fetch api 或設定計數器等，最後則會將取得的資料更新到頁面上。

## 2. Updating

### static getDerivedStateFromProps\(nextProps, prevState\)

組件開始載入（render）前被調用，以及每次父組件 props 更動時，也會調用此方法。此方法接收兩個參數，第一個為要更新的 props，第二個則為舊的 state 值。

此方法通常用在，子組件 state 會根據父組件的 props 改變，且當父組件 props 更新時，便可在此更新 state，但父組件有可能在沒有更新 props 的情況下，重新 render 此組件，因此子組件中，便可透過此方法，比較 nextProps\(新的 props\) 和 prevState\(舊的 state\) 有無差異，若無差異，便回傳 null 表示不更新。如下所示：

```javascript
static getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.title != prevState.title) {
    return {
      title: nextProps.title 
    };
  }
  return null;
}
```

**程式碼說明**  
1. 第2-6行程式碼，把新的props\(nextProps.title\)和舊的state\(prevState.title\)做比較。 
2. 第3-5行程式碼，當nextProps和prevState不相同時，回傳新的title state。 
3. 第7行程式碼，當nextProps和prevState無差異時，回傳null不更新state。

### shouldComponentUpdate\(nextProps, nextState\)

當props或state要更新時，便會觸發此方法，並回傳（return）true表示要重新render頁面，或回傳false表示不render頁面，而其接收兩個參數，第一個為要更新的props，第二個則是要更新的state。

此方法通常用在，避免頁面不必要的重新render，此方法比較this.props和nextProps，及this.state和nextState的差異，決定是否重新render頁面，如下所示： 

``` javascript 
shouldComponentUpdate(nextProps, nextState) { 
  if (this.state.title != nextState.title) { 
    return true;
  } 
  return false
}
```
範例說明 
1. 第2-4行程式碼，透過this.state取得舊的title值，並和新的nextState.title比較。 
2. 第3行程式碼，當this.state.title和nextState.title不相同時，回傳true，確認要render頁面。 
3. 第5行程式碼，當this.state.title和nextState.title相同時，回傳false，不重新render頁面。

### getSnapshotBeforeUpdate\(prevProps, prevState\)

重新render頁面後，在渲染頁面前調用此方法，此方法在一般開發並不常使用，通常用在處理較特殊的問題，像是頁面滾動（Scroll）的位置等，此方法會回傳一個更改後的值，並在componentDidUpdate\(\)接收，做適當的修改。

### componentDidUpdate\(prevProps, prevState, snapshot\)

重新render完頁面，便會觸發此方法，其中第三個參數snapshot便是由getSnapshotBeforeUpdate\(\)所傳遞的資料。

## 3. Unmounting

### componentWillUnmount\(\)

當組件要從頁面上被移除時，也就是說使用者離開頁面前，會調用此方法，適合用來處理離開頁面後的關閉監聽或是計時\(timer\)等清理工作。

---

如果這篇文章對你有幫助，可以前往 [Github react-implement](https://github.com/weichinhsu/react-implement) 按下 Star 來支持我，我會不定期的更新教學內容。
也可以 follow 我的 Github 帳號，未來我也會繼續寫更多的網頁技術與大家分享！