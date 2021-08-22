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