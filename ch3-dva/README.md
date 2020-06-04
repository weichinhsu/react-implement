# Ch3 Dva 架構

本章節便要開始加入 Dva 的概念，將程式依照不同的工作性質分工，不再是把所有的邏輯通通寫在同一個頁面上，造成可讀性下降，而在維護程式時，也能夠快速地找到問題所在。

Dva 是一個由 Redux 所衍伸而來框架，目的是實作出簡單又易操作的程式框架，由於在一個 React 的應用程式中，state 是不可或缺的部分，不管是在頁面上記錄的狀態，或是不同元件，甚至不同頁面中互相傳遞的狀態，因此當應用程式越來越大，頁面上的組件或需要處理的邏輯程式也越來越多時，便會造成 state 過於複雜，且難以管理，這時候便可以透過 Dva 來簡化這些複雜的工作。

> [dvajs](https://github.com/dvajs/dva)  
> Lightweight front-end framework based on redux, redux-saga and react-router.

## Dva 觀念

#### Dva基本流程

一個最基本的流程包含了 View 頁面、Model 以及 State 狀態，下圖可以看到，從 View 頁面發送 Action 動作請求，而 Model 接收到動作後，便會透過 Reducer 處理請求資料，完成後更新儲存在 State 中的資料，而當 State 的資料更動了，就會重新渲染頁面上的組件，如此便是一圈完整的 Dva 運作流程。

為了讓讀者可以更清楚的了解整個流程，我們以待辦清單專案為例來說明，當使用者在頁面上輸入待辦項目，按下確認按鈕後，便會發送一個Action到Model中的Reducer處理，完成後更新State的待辦清單資料，最後會重新渲染頁面，將待辦事項顯示在頁面上。

#### Dva處理非同步流程

當需要處理非同步問題時，流程便會如下圖，當View發送Action請求時，會由Model的Effect處理，此時Effect會發出HTTP向Server後端請求資料，接著由Reducer將取得的資料更新State並重新渲染頁面即完成流程。

這邊同樣也以例子來說明，在登入某個網頁時，在頁面輸入帳號密碼，點下登入按鈕後，頁面會發送一個登入 Action，而 Model 的 Effect 接收到，便會開始進行 HTTP 請求，向後端發送登入要求，當後端驗證使用者帳號密碼成功後，返回使用者資料，此時 Effect 便會將取得的資料給 Reducer，進行儲存及更新 State，最後刷新頁面顯示登入成功及使用者資訊。

其中這邊的 Effect，便是由 redux-saga 所提供的解決非同步問題的辦法。

> [redux-saga  
> ](https://github.com/redux-saga/redux-saga/)是一個 Dva 的中介層（Middleware）應用，主要是用來處理像是 HTTP 請求時，會遇到的非同步問題。

> 非同步 Asynchrony   
> JavaScript 是一種非同步的語言，程式不需要一個指令一個步驟的執行，表示非同步的語言執行程式時，可能會同時執行多行程式碼，反之同步 \(Synchrony\) 的程式語言，則是要一行一行的執行。  
> 由於 JavaScript 的非同步特性，在請求 HTTP 時，因為需要等待後端回覆資料，便很有可能會發生程式尚未取得後端的資料，但後面的程式卻已經執行，造成無資料可以處理的錯誤，這便是一般常見的非同步問題。



