# Ch1 React 介紹

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
