# 建立第一個 React 專案

本章節開始教導讀者如何建立一個 React 專案，以及如何在瀏覽器上運行專案。

## 1. 建立專案
首先開啟終端機

**1. 使用 npx 指令建立第一個 React 專案**
```
cd Desktop
npx create-react-app my-first-project
```
**指令說明** <br>
1. 在桌面建立專案，因此透過 cd 指令進入桌面路徑。
2. 上透過 npx 去執行 create-react-app 指令，來建立 React 專案，並命名為 my-first-project 。

**2. 進入專案**
```
cd my-first-project
```
**指令說明** <br>
透過 cd 指令進入專案中。

---
### 補充筆記：cmd 常用指令 cd
在開發時， 時常會用到 windows 中的命令提示字元（cmd），因此讀者若熟悉一些常用的指令，便可以提升學習速度。

由於命令提示字元視窗預設的路徑為使用者名稱資料夾，如下所示：
```
C:\Users\ 使用者名稱>
```
但一般開發時，並不會直接在此目錄下建立專案，因此常常會需要變更路徑位置，此時便可以透過「cd + 目錄位置」，進入指定的資料夾目錄下。

但要注意的是，指定的目錄位置必須是當前目錄下存在的資料夾，例如在使用者名稱的資料夾下通常會有 Desktop(桌面)資料夾，因此只要輸入下列指令即可進入桌面：
```
cd Desktop
```
若是我們指定的目錄位置在使用者名稱資料夾下不存在時，在視窗上便會顯示「系統找不到指定的路徑。」的訊息。

---


**3. 執行專案**
```
npm start
```

完成後，便會自動開啟網頁瀏覽，若沒有自動開啟，也可以自己開啟瀏覽器，並在網址列輸入 http://localhost:3000/ 便可以進入頁面。

## 2. 專案結構
```
├──node_module/       # JS 套件庫（JS Libraries）
├──public/            # Static file
├──src/               # 專案漲
    ├──App.js         # 預設第一個頁面
    ├──index.js       # 預設 React 專案入口
├──package.json       # JS相依性紀錄檔
└──package-lock.json  # 檢驗套件版本
```
詳細專案檔案目錄解說分述如下：

* **node_module** <br>
  在專案中一些必要的模組，以及透過npm 安裝的套件都會存放在此資料夾中，這邊需要注意的是，一般開發時，為了避免一些錯誤發生，通常不會直接修改此目錄中的檔案。

* **public** <br>
  放置靜態或是不會被更動的檔案，例如網頁設定、描述或 Icon 等。

* **src** <br>
  存放專案檔的資料夾，之後我們所寫的檔案幾乎都會放置在此資料夾下，方便專案的管理，其中 App.js 是 React 建立專案後預設的元件，詳細元件的使用方式將會在之後介紹，而 index.js 是整個專案的程式進入點，詳細的設定方式也會在後面的章節介紹。
  
* **package.json** <br>
  在package.json 中主要存放一些專案的資訊，例如專案名稱、版本及描述等，未來若有在專案中安裝套件，也都會顯示在此檔案中，其他詳細說明將會在介紹。

* **package-lock.json** <br>
  package-lock.json 是在npm5 之後才推出的， 當node_modules 或package.json 發生變動時會自動生成文件，並檢驗版本是否吻合，且每次npm install 或update 時都會進行更新。

## 3. 程式進入點 index.js
此檔案為 React 專案啟動時的進入點，運行專案時，會負責將應用程式的資訊顯示在頁面上，預設沒有使用任何架構，本書在後面章節使用 Dva 架構時，也會在這裡設定，因此目前了解基本的設定即可，如下所示：
``` javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

serviceWorker.unregister();
```
**程式碼說明**
1. 第1-2行程式碼，引入 React、ReactDOM 元件。
2. 第3行程式碼，CSS 樣式。
3. 第4行程式碼，引入 APP 元件。
4. 第3行程式碼，引入app.json設定檔中的name參數，並命名為appName表示應用程式要顯示的名字。
5. 第5行程式碼，This optional code is used to register a service worker. register() is not called by default. This lets the app load faster on subsequent visits in production, and gives it offline capabilities.
6. 透過 render 方法將 APP 元件渲染到 root element 上。
7. StrictMode 元件是 React 的嚴格模式，用來突顯應用程式裡潛在問題的工具（可不寫），它不會 render 任何可見的 UI。

## 4. App.js
建立專案後預設的第一個頁面元件。
```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    ...
  );
}

export default App;
```
**程式碼說明**
1. 建立 APP 元件。
2. export default 將 APP 元件輸出。

---
### 補充筆記 export / export default
在 JavaScript 中可以透過 export 語法來**匯出**程式模組（Module），讓其他的檔案可以讀取此模組，因此這邊介紹幾個 export 重點，如下：

一個檔案可以 export 很多個模組
``` javascript
export function A(){ }
export function B(){ }
export function C(){ }
```

但一個檔案只能 export default 一個模組
``` javascript
export default function A(){ }
```

export 可以分開寫
``` javascript
function A(){ }

export default Ａ
```

---
### 補充筆記 import 

在 JavaScript 中可以透過 import 語法來引入程式模組，並且會搭配 export 或 default export 使用， 在 React 中import是很常見的引入方式，因此這邊介紹幾個 import 重點，如下：

**第一種方式** <br>
由大括號的方式引入的模組，表示 test01 元件中有 export 三個模組，注意引入的名稱必 須跟 test01 元件中 export 的名稱相同。
``` javascript
import {A, B, C} from 'test01';
```
test01.js
``` javascript
export function A(){ }
export function B(){ }
export function C(){ }
```

**第二種方式** <br>
直接引入模組，表示 test02 元件中有 default export 的模組，使用此方式 import 的名稱不需跟 test02 元件中 export 的名稱相同。
```javascript
import Apple from 'test02';
```
test02.js
``` javascript
export default function A(){ }
```
**as 命名** <br>
透過 as 可以為引入的模組取名，如下，將A模組重新命名為 MyApp，注意命名只適用在第一種引入方式，不適用在第二種。
```javascript
import {A as MyApp, B, C} from 'test01';
```

**json 引入** <br>
如果引入的檔案是json檔，此json檔就不需要export或default export，import可直接引入即可。
```javascript
import data from 'jsonFile';
```
jsonFile.json
```javascript
[{
  'a':1,
  'b':2,
},{
  'a':3,
  'b':4,
}]
```
---

## 5. 補充筆記 package.json
package.json 檔案是以 JSON 格式來存放專案的一些資訊，包含專案描述、自訂指令或安裝套件紀錄等，而本小節將會針對安裝套件紀錄詳細說明，也就是檔案中的 dependencies 區塊。
dependencies 區塊為記錄此專案依賴的套件，也就是此專案中所安裝的套件模組，主要是紀錄套件名稱及安裝的版本，如下所示：
```
"dependencies": {
  "react": "^16.13.1",
  "react-dom": "^16.13.1",
}
```
這邊值得注意的是，若讀者是從網路上取得他人分享的 React 的專案時，通常都不會有 node_modules 資料夾，因為 node_modules 下都是存放依賴套件的內容，會讓整個專案的大小變得十分龐大，為了避免這樣的問題，我們會先將 node_modules 刪除，再傳送至網路上或給其他人。

因此當取得他人的專案時，必須先在專案目錄下執行安裝套件指令，如下，此時 npm 會搜尋 package.json 中記錄在 dependencies 的套件，並判斷套件名稱及版本才會安裝到此資料夾下。
```
npm install
```
當要解除安裝套件時，可以透過 npm uninstall 加上要刪除的套件名來刪除，如下所示：
```
npm uninstall react
```
指令說明
執行上述指令後，便會將 react 套件解除安裝，同時也會將套件名稱從 dependencies 中移除。
若未來讀者要安裝其它套件時，也可以透過 npm install 來安裝，並在指令後方加上「--save」參數，這邊以安裝 react 套件為例，如下所示：
```
npm install --save react
```
指令說明
上述指令除了會安裝 react 套件之外，也會將 react 套件名稱與版本新增到 dependencies 中，但若沒有加上「--save」參數，則此套件的名稱可能不會出現在 dependencies 中，而此用意，除了讓開發者可以方便的管理專案套件之外，也可以讓安裝在自己電腦的專案，移動到其他電腦時，只需要在專案根目錄下執行 npm install，就會自動安裝 package.json 清單中相關的套件，避免有些套件沒有安裝到，而造成運行錯誤。

上述範例主要目的是讓讀者了解，如何安裝以及解除安裝套件，因此若讀者有接續著專案進行練習的話，要記得將 react 套件安裝回來唷！
