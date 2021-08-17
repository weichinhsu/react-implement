# Redux 概念

本小節將要帶讀者了解如何實際應用 Redux 觀念。

## action 與 dispatch
在Redux中，action是用來觸發Reducer流程的一個重要物件，而dispatch則是用來發送action的一個方法，因為有兩種機制的配合，才能讓Redux的流程順利的完成，接下來將會分別介紹兩種概念。

### 觸發流程物件：action
action中文意思為動作，在Redux中，表示要觸發更新資料的動作，每一個action都是物件組成，並擁有一個type屬性，並設定Reducer的名稱，用來判斷要進入哪一個Reducer，除此之外，也可以加入payload屬性，將資料傳送到Reducer，並更新Store中的資料。常見的action格式，如下所示：

``` javascript
{
  type: 'REDUCER_NAME',
  payload: data
}
```
**程式碼說明**

設定action的type與payload屬性，注意type為action之必要屬性，而若沒有要傳遞資料時則可省略payload。

**發送action方法：dispatch**

有了觸發流程的action後，也需要一個用來發送動作的方式，這便是dispatch的工作，它是由Redux Store提供的方法，可以將action配送給Reducer，以完成更新Store的動作。dispatch方法的使用方式如下：

``` javascript
dispatch({
  type: 'REDUCER_NAME',
  payload: data,
})
```
**程式碼說明**

將要傳送的action放入diapatch方法中即可觸發該動作。

看到這裡若讀者對action和dispatch還有疑惑，可以將action想成一封公司寄給員工信，信中的type紀錄送達員工的姓名，payload則是紀錄在信中的工作內容，而傳送此封信的人就是dispatch，可以想成是郵差或是送信者，當信送達後，員工便可以依照信中的內容去完成工作。

本小節簡單說明了action與dispatch的使用方式，其他更詳細的dispatch實現方式將會在後續與讀者介紹。

## Action Creator 處理資料

在Action Creator流程中，主要是用來負責處理頁面傳送過來的資料，必要時會發送HTTP請求，並將處理完成的資料傳送給Reducer儲存，接下來介紹Action Creator的使用方式。

首先會先建立一個Action Creator Function，如下所示：
``` javascript
export const setMessage = (message) => {
  return {
    type: 'UPDATE',
    payload: message 
  }
}
```
**程式碼說明**

從上述程式碼可以看到，setMessage便是一個ActionCreator，在這個方法中，我們可以對資料進行處理，完成後，便回傳(return)要更新資料的action，並帶入要觸發Reducer的type與要更變的資料。

## Reducer儲存資料

設定完成 Action 後，便可以開始撰寫 Reducer 方法，接收要變更的資料，並更新 Store。這邊值得注意的是，在Reducer 中的程式要越單純越好，它只負責接收並更新資料，因此資料處理邏輯應在Action流程處理完成後才傳給Reducer儲存。接下來介紹Reducer的使用方式，如下所示：

``` javascript
export default (state = "", action) => {
  switch (action.type) {
    case 'UPDATE':
      return {
        message: action.payload
      }
    default:
      return state
  }
}
```
**程式碼說明**
1. 第1行程式碼，設定state的初始值。
2. 第2-3行程式碼，判斷action的type是否相同。
3. 第4-6行程式碼，當case中的UPDATE字串與前一小節所發送的action type相同，便能成功更新儲存在Store的message資料。
4. 第7-8行程式碼，當不符合UPDATE字串時，則回傳原本的資料，不做更動。

## Store資料格式
Store在Redux中是儲存資料的地方，每應用程式只會有一個Store，讀者可以把它想成是一個大倉庫，裡面以物件（Object）格式存放著應用程式中會使用到的資料，如下所示：
``` javascript
var store = {
  state1: {
    name : 'John',
    age : 20
  },
  state2: {
    name : 'Amy'
  }
}
```
**程式碼說明**

由上述程式片段可以看到，不同的 State均儲存在單一 Store 中，當更新某個State時，所有有取用此 State 的頁面將會重新渲染。

# React Redux

由於 Redux 是一個獨立的函式庫，並不是特別為了 React 所設計，它也可以應用在 Angular、jQuery 或是 JavaScript 等其他框架上，而為了讓 Redux 在 React 中，可以更方便的操作，Redux 官方開發了另一個函式庫 React Redux，讓 React 和 Redux 可以快速的結合起來，讀者可以把它想像是一個橋梁的作用，讓兩邊的資料可以交互使用。

接下來，我們必須了解 React Redux 提供了哪些重要的功能，連結了 React 和Redux，例如它讓原本 React 中的 Component 元件，可以讀取 Redux Store 的資料，因此這邊介紹了最基本的功能，如下所示：

## Component

### Provider
`Provider` 主要是讓所有 Component 可以取得儲存在 store 的資料，其形式大致如下:
``` javascript
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import { store } from './app/store'
import { Provider } from 'react-redux'
import * as serviceWorker from './serviceWorker'
import App from './App'

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
)
```
**程式碼說明**

1. 第4行程式碼，import在`'./app/store'`中定義好的store。
2. 第5行程式碼，從 `react-redux` 中引入 `Provider。`
3. 第11-13行程式碼，透過 `Provider` 將 store 綁定給頁面，讓 App 元件能夠存取 store 中的資料。

## Hook
接下來會介紹幾個在 redux 中重要的 Hook，讓我們可很容易存取 store 的資料。

### useSelector
用來取得存在 store 中的 state，呼叫後會回傳指定的 state，範例如下：

``` javascript
import React from 'react'
import { useSelector } from 'react-redux'
import { RootState } from './store'

export const CounterComponent = () => {
    const counter = useSelector((state: RootState) => state.counter)
    return <div>{counter}</div>
}
 ```

 如果不想在每次使用 `useSelector` 都要指定 root state 的類型時，就可以使用 `TypedUseSelectorHook` 為 root state 建立一個適合的類型，範例如下：

 ``` javascript
import React from 'react'
import { useSelector } from 'react-redux'

export const CounterComponent = () => {
    const counter = useSelector((state) => state.counter) // 不需要在指定root state的類型
    return <div>{counter}</div>
}
 ```

**TypedUseSelectorHook**

建立一個符合 store 的 root state 類型的 hook。
當沒有特定類型的 state 時，可以使用 `TypedUseSelectorHook` 來自動建立一個適合的當前 root state 的類型，範例如下：

``` javascript
interface RootState {
    property: string;
}

const useTypedSelector: TypedUseSelectorHook<RootState> = useSelector;
 ```

### useDispatch
用來連接 redux 的 dispatch 方法，呼叫 `useDispatch` 後會回傳一個 dispatch 方法，範例如下：

``` javascript
import React from 'react'
import { useDispatch } from 'react-redux'

export const CounterComponent = ({ value }) => {
    const dispatch = useDispatch()
    return (
        <div>
            <span>{value}</span>
            <button onClick={() => dispatch({ type: 'increase-counter' })}>
                Increase counter
            </button>
        </div>
    )
}
```

