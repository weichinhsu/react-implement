# 3-1 Model 的格式與操作

接下來本小節要開始介紹 Dva 最重要的 Model 觀念，首先，讓我們先了解 Model 的架構，Model 結合了 Reducer、Action 與State等核心，讓我們看到以下Model程式架構：

```javascript
export default {
  namespace: 'modelName',
  state: { ... },
  reducers: { ... },
  effects: { ... }
}
```

從上述程式碼中可以看到，Model 主要是以 key-value 的方式定義，一般常用的屬性主要包含四個，分別為 namespace、state、reducers 與 effects，接下來將會一一介紹每個屬性的意義與撰寫方式。

#### namespace

namespace 顧名思義就是用來設定 Model 的名稱，在頁面上若要操作此 Model 中的資料時，便會需要發送此 namespace，讓程式可以辨識資料的位置。

#### state

設定 state 初始值的地方，格式如下所示：

```javascript
state: { 
    state01: null, 
    state02: 10 
}
```

**程式碼說明**  
以 key-value 的方式儲存 state 資料。

#### reducers

是整個運作流程中唯一可以修改 State 的地方，而呼叫 Reducer 的方式主要是透過 action 觸發，reducer 格式如下：

```javascript
reducers: {
  SET_data(state, { payload }) {
    return {
      ...state,
      data: payload
    }
  }
}
```

**程式碼說明**

1. 第 2 行程式碼，建立一個名為 SET\_data 的 Reducer，並傳入兩個參數，第一個 state 為儲存在此 Model 的所有資料，第二個參數則是透過 JS ES6 解構（Destructure）的特性將 action 傳送的 payload 資料取出。
2. 第 3-6 行程式碼，將資料儲存並回傳，其中儲存方式也是透過 JS ES6 展開運算符（Spread Operator）的特性達成，表示將保留原有 State 的其他資料，只更新 data 值。

> **解構 Destructure**
>
> JavaScript 在 ES6 中提出了解構的特性，將一般陣列與物件取值的方式簡化許多，同時也提高了程式的閱讀性，這邊直接以例子的方式與大家說明。在 ES6 之前，當要取得物件中的某個值時，便需要額外宣告變數，再給予指定的值，如下所示： 
>
> `const obj = { a: 1, b: 2, c: 3 }   
> const value = obj.b   
> console.log(value) // 2` 
>
> 而在 ES6 後，提出了解構的特性，簡化了物件取值的方式，如下所示：
>
>  `const { b } = { a: 1, b: 2, c: 3 }   
> console.log(b) // 2`

> **展開運算子 Spread Operator** 
>
> JavaScript 在 ES6 中提出了展開運算符的特性，簡化了物件與陣列展開的過程，讓使用者可以更容易的合併、複製、存取陣列與物件，這邊直接以例子的方式與大家說明。在 ES6 之前，合併兩個陣列時，便需要使用 concat 方法，如下所示： 
>
> `const array1 = ['a','b','c']   
> const array2 = ['d','e','f'] console.log(array1.concat(array2)) // ["a", "b", "c", "d", "e", "f"]` 
>
> ES6 之後，使用展開運算子合併陣列，如下所示： 
>
> `const array1 = ['a','b','c']   
> const array2 = ['d','e','f'] console.log([...array1,...array2]) // ["a", "b", "c", "d", "e", "f"]` 
>
> 也可以使用在存取物件的數值上，如下所示： 
>
> `let obj={ a: 1, b: 2, c: 3 }   
> var save = { ...obj, b:4 };   
> console.log(save); // {a: 1, b: 4, c: 3}   
> var insert = { ...save, d:5 };   
> console.log(insert); // {a: 1, b: 4, c: 3, d: 5}` 
>
> **程式碼說明**   
> 上述程式碼可以看到透過展開運算子，不但可以更新物件中 b 的值，也可以新增物件的值。

#### effects

主要用來處理 HTTP 請求的非同步問題，以及發送 action 觸發 Reducer，要注意的是 Effect 中的方法是以 JS ES6 的 Generator Function 的方式來定義，格式如下：

```javascript
effects: {
  * GET_data({ payload }, { put, call, select }) {
    yield put({ type: 'SET_data', payload: payload })
  }
}
```

程式碼說明

1. 第 2 行程式碼，建立一個名為 GET\_data 的方法，並接收兩組參數，第一個是將 action 傳送的 payload 資料傳入，第二個則是傳入三個方法，分別為 put 可以發送 action 觸發 Reducer、call 可以發送 HTTP 請求，以及 select 可以取得所有 State 資料。
2. 第 3 行程式碼，以 put 方法為例，表示發送一個 action，指定 Reducer 為 SET\_data，並將payload資料傳送至 Reducer 儲存。

> Generator Function
>
> JavaScript在ES6中提出了Generator Function的特性，是用來解決非同步問題的方法，其最特別的用法便是使用yield關鍵字，表示在方法中遇到yeild時會暫停執行，並進入呼叫的方法中執行，直到呼叫的方法執行完畢，以React Native的例子來說，如下所示：
>
> `GET_data({ payload }, { put, call, select }) {  
>   yield put({ type: 'SET_data', payload: '123'})  
>   yield put({ type: 'SET_list', payload: '456'})  
> }`
>
> **程式碼說明** 
>
> 上述程式碼可以看到在 GET\_data 方法中，當方法執行時遇到第一個 yeild 後，便會暫停繼續往下執行，並進入 put 方法，將資料發送給 Reducer 儲存，直到儲存完成，才會返回 GET\_data 方法繼續執行後面的程式碼，以此類推。

#### 在頁面上呼叫Model

Model設定完成後，如何在頁面上呼叫Model中的方法呢？是透過dispatch發送一個action，去觸發Model的方法，如下所示：

```javascript
this.props.dispatch({
    type: 'model_name/model_function',
    payload: data,
    callback: () => { }
})
```

**程式碼說明**

1. 第 2 行程式碼，設定 action 的 type，格式為 Model 的 namespace 加上 Model 中的方法，中間以「/」分隔，注意type為action必要之屬性。
2. 第 2-3 行程式碼，設定要傳送的 payload 資料或 callback 方法，注意這兩個部分並非 action 必要之屬性，讀者可以依照開發需求調整。

