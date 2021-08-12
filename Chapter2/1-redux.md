# React Redux

由於Redux是一個獨立的函式庫，並不是特別為了React所設計，它也可以應用在Angular、jQuery或是JavaScript等其他框架上，而為了讓Redux在React中，可以更方便的操作，Redux官方開發了另一個函式庫React Redux，讓React和Redux可以快速的結合起來，讀者可以把它想像是一個橋梁的作用，讓兩邊的資料可以交互使用。

接下來，我們必須了解React Redux提供了哪些重要的功能，連結了React和Redux，例如它讓原本React中的Component元件，可以讀取Redux Store的資料，因此這邊介紹了最基本的功能，如下所示：

**Provider**
Provider主要是讓所有有經過connect方法與 Redux Store 連結的元件可以取得儲存在 store 的資料，其形式大致如下:
``` javascript
import React, { Component } from 'react';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import HomePage from './src/homePage';

const store = createStore();

export default class App extends Component {
  render() {
    return (
      <Provider store={store}>
        <HomePage />
      </Provider>
    );
  }
}
```
**程式碼說明**

第2行程式碼，從react-redux中引入Provider。
第3行程式碼，從redux中引入createStore。
第6行程式碼，透過createStore方法，建立Store儲存空間。
第11-13行程式碼，透過Provider將store綁定給頁面，讓HomePage元件便能夠存取store中的資料。

# Redux 概念

了解Redux的概念後，本小節將要帶讀者了解如何實際應用這些觀念，並依照前面提到的Redux流程依序介紹Component與Container、action與dispatch、Action Creator、Reducer以及Store。