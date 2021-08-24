# Redux toolkit

## Store
### configureStore
設定 store，可以將多個reducer綁定，形成一個root reducer。
範例如下:

``` javascript
import { configureStore } from '@reduxjs/toolkit';
import myReducer from '../path/to/slice';
import yourReducer from '../path/to/slice2';

export const store = configureStore({
  reducer: {
    my: myReducer,
    your: yourReducer 
  },
})
```

**ThunkAction**
[ThunkAction](https://stackoverflow.com/questions/63881398/how-to-properly-type-a-thunk-with-thunkaction-using-redux-thunk-in-typescript)

**Action**
如同前面提到的action是一個 [plain object](https://stackoverflow.com/questions/52453407/the-difference-between-object-and-plain-object-in-javascript)，目的是用來改變state的值。
在頁面上任何會操作到資料的事件、網路請求等等都需要透過action來觸發。
除此之壞，每個action都必須有一個type欄位，用來表示目前正在執行的動作類型。而其他在action中的欄位則可以隨著不同的需求自行設定。

常見的action格式，如下所示：

``` javascript
{
  type: 'TYPE_NAME',
  payload: data
}
```


## Reducer

**createSlice**
用來設定state初始值、建立reducer方法、命名slice等，createSlice會自動建立action creator和action type。
createSlice接收一個物件參數，並且包含幾個重要的key，如下所示：
* name(required): 命名此slice
* initialState(required): 設定state初始值
* reducers(required): 建立reducer方法
* extraReducers(optional): 處理在其他地方已經定義好的action，例如 `createAsyncThunk` action。

一個簡單的createSlice範例如下，我們建立了一個名為counter的slice，並設定初始的value state為0，接著定義一個reducer方法increment。
因此在頁面上透過dispatch發送increment時，便會將value的值加1。

``` javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState: CounterState = {
  value: 0,
};

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  // 定義reducer function並建立相關的action
  reducers: {
    increment: (state) => {
      // Redux Toolkit 使用 Immer library 來處理 state 的變動
      state.value += 1;
    },
  },
})
```

**createAsyncThunk**
我們通常會使用createAsyncThunk來建立一個HTTP請求的action。
createAsyncThunk是based on一個叫redux-thunk的package，它會幫我們處理HTTP請求非同步的動作。而在Redux Toolkit中，將redux-thunk的功能整合進來，因此我們不需要再而外去安裝redux-thunk，直接使用createAsyncThunk即可。
而createAsyncThunk主要接收兩個參數，第一個是要建立的action名稱，第二個則是要處理的非同步方法。

``` javascript
export const incrementAsync = createAsyncThunk(
  'counter/fetchCount',
  async (amount: number) => {
    const response = await fetchCount(amount)
    return response.data
  }
);
```


**PayloadAction**


