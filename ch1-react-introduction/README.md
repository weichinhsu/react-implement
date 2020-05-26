# Ch1 React 基礎

隨著世代的進步，不管是 Web 或是行動裝置的前端程式開發，都越來越受矚目，當然要求也就變的更為嚴苛，不再像是過去單純撰寫 Html、CSS 及 JavaScript 就可以滿足，而為了達到互動式的效果，以提升使用者體驗，同時也要顧及跨瀏覽器和跨平台使用的需求，往往會讓開發的複雜度增加許多，因此便衍伸出許多讓開發更直覺的前端框架（Framework）或函式庫（Library），例如 React、Angular、Vue 等。

在各式的 JavaScript 框架或函式庫中，React 是由 Facebook 在 2013 年所開源的函式庫，並將 React 定位為「A JavaScript library for building user interfaces.」，表示是用來建立 UI 的 JavaScript 函式庫，而它的技術概念，也為前端開發帶來許多不同的影響，例如：Component 元件的觀念、單向資料流等觀念，也讓 React 在前端技術中佔有一席之地。隨著時間的發展，至今 React 已逐漸形成一個完整的生態圈，讓開發者擁有更好個開發環境，接下來將會簡單的介紹 React 生態圈的組成。

## ReactJS

ReactJS是一個以JavaScript為底的函式庫，可以輕鬆的建立互動式的UI介面，其原本的主軸是Web網頁開發，而後慢慢擴展出行動端（React Native）、伺服器端（react-server），甚至是VR領域（react-360）。

而ReactJS不同於以往前端開發的特色如下：

* 單向資料流：透過單向資料流，可以減少程式的複雜度，不同於傳統JavaScript綁定資料的方式，可以降低資料的重複性。
* Component元件的觀念：透過元件，將重複的程式碼打包成元件，並在需要時再引入呼叫即可，同樣也可以降低程式的重複及複雜度。
* Virtual DOM：ReactJS透過Virtual DOM與網頁的DOM溝通，它會在渲染頁面時，檢查上次頁面的狀態，最後只會將有差異的部分更新，與傳統JavaScript更動頁面時，會將整個頁面重新繪製不同，因此可以大幅提升效能。

## NPM/NPX

NPM（Node Package Manager）是由Node.js預設，並以JavaScript編寫的軟體套件管理系統，它簡化了在專案中套件安裝、升級和解除安裝等麻煩過程，而在React生態圈中，它除了可以用來建構專案，同時也可以在專案中，安裝各式不同的套件。

而NPX則是NPM v5.2.0版本後新增的指令，它可以讓使用者避免全局安裝任何東西，其他NPM與Node.js使用方式會在之後使用到時與讀者說明。

## JSX語法

在React中使用JSX語法來撰寫，而JSX並不是一個新的語言，它是一個語法糖（Syntatic Sugar），相較於HTML語法，JSX更接近XML語法，它可以自訂標籤，讓程式看起來更直觀，如下：

**HTML語法**

```javascript
<div id="Content">
  <p>Hello</p>
</div>
```

**JSX語法**

```javascript
function Content(props) {
  return 
    <div id="Content">
      <p>Hello</p>
    </div>
}
```

上述程式碼可以看到，在JSX語法中，自訂了一個Content標籤，相較於HTML語法3行的Content更簡潔，倘若須要重複Content，在JSX中只要再次呼叫Content標籤即可，但在HTML中卻要重複3行程式碼，因此JSX也讓程式減少許多重複的語法，而Content也是React中Component元件的概念，其定義方式將會在後面章節介紹。

除此之外，JSX採用了聲明式（declarative）的撰寫風格，簡單來說就是讓程式邏輯和原件可以搭配使用，如下：

```javascript
const Message = () => {
    return <p>Hello</p>
}
const Content = () => {
  return 
    <div id="Content">
      { Message() }
    </div>
}
```

上述程式碼可以看到宣告一個方法Message，並且回傳文字，表示當須要用到此元件時，呼叫Message方法即可。

接著來看採用命令式（Imperative）撰寫風格的傳統HTML，以及JavaScript，便只能分開撰寫，如下：

**HTML檔**

```javascript
<div id="Content">
</div>
```

**JavaScript檔**

```javascript
const node = document.createElement("p");
const textnode = document.createTextNode("Hello");
node.appendChild(textnode); 
document.getElementById("Content").appendChild(node);
```

由上述程式碼，可以明顯地感受到JSX語法讓程式語言更簡潔，可讀性十分的高，因此在開發程式時，便可以方便開發人員更加的快速撰寫。

## JavaScript ES6+

在 React 生態系中，是使用 JavaScript ES6（ECMAScript 6）以上的版本為主要開發的語言，因此若讀者只有 ES5 的基礎，對於開發 React 相關的專案來說，可能時常會看到一些較過去不同的語法，所以本書也建議讀者在學習 React 之前，可以了解 JavaScript ES6 版本以上的語法，往後在開發 React 也會較易上手。

## Flux/Redux/Dva概念

Flux 是一個由 Fackbook 提出的單向資料流概念，而 Redux 則是實作出 Flux 的概念，透過 Redux 框架，在程式中便可以更輕鬆的管理狀態（state），最後 Dva 是改善了 Redux 的缺點後所發展出來的架構，本教學也會以 Dva 為主要使用架構。

## React Native

一般說到 React，一定也會聽過 React Native，它是 React 在 2015 年推出的行動端（Mobile）框架，它可以讓開發者透過 React 和 JavaScript 撰寫出類似原生（Native）程式的應用程式，因此在其發行後，便受到許多開發者的歡迎。

繼續閱讀

* [我的第一個 React 專案](https://github.com/weichinhsu/react-implement/blob/master/Ch1%20React%20Introduction/1-first-react-project.md#%E5%BB%BA%E7%AB%8B%E7%AC%AC%E4%B8%80%E5%80%8B-react-%E5%B0%88%E6%A1%88)
* [Component 元件](https://github.com/weichinhsu/react-implement/blob/master/Ch1%20React%20Introduction/2-component.md#react-%E5%9F%BA%E7%A4%8E--component-%E5%85%83%E4%BB%B6)
* [State v.s. Props](https://github.com/weichinhsu/react-implement/blob/master/Ch1%20React%20Introduction/3-props-and-state.md#react-%E5%9F%BA%E7%A4%8E--props-%E8%88%87-state) 
* [生命週期](https://github.com/weichinhsu/react-implement/blob/master/Ch1%20React%20Introduction/4-lifecycle.md#react-%E5%9F%BA%E7%A4%8E--%E7%94%9F%E5%91%BD%E9%80%B1%E6%9C%9F)

