# 第一個 Redux 專案

本小節以一個簡單的留言板為範例，從介紹如何安裝Redux、專案環境到整個完整的Redux的流程，讓讀者可以更了解程式邏輯的運作過程。

> 本專案主要會以 Redux TypeScript 來說明，有時間的話也會寫一個 JavaScript 的版本ＸＤ

## 建立專案

首先開啟終端機，建立一個新的專案，我們使用官方已經定義好的redux-typescript template 來快速建立一個 Redux 專案，指令如下：
```
npx create-react-app my-redux-app --template redux-typescript
```
透過redux-typescript這個template，他會幫你把必要的redux和typescript的套件都裝好，我們只需要再額外裝一些自己習慣用的開發套件即可，可以省去許多安裝的時間。

[Reference: redux-typescript template github](https://github.com/reduxjs/cra-template-redux-typescript)

建立完成後，輸入下列指令進入專案中，指令如下：
```
cd my-redux-app
```
接著透過npm，開始安裝一些我們之後會使用到的實用套件：
```
npm install react-router-dom
npm install antd                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
```
套件說明
1. react-router-dom: 路由工具，我們之後會使用此工具來實作跳頁功能。
2. antd：全名為Ant Design，提供許多精美的Coomponent，讓我們在開發時可以直接套用，不用自己花時間撰寫。

[react-router-dom Github](https://github.com/join?return_to=%2Fweichinhsu%2Freact-implement&source=login)

[Ant Design 官網](https://github.com/join?return_to=%2Fweichinhsu%2Freact-implement&source=login)

完成後，我們就可以透過 `npm start` 跑看看專案啦！

在網頁上瀏覽專案就可以看到預設的範例是一個計數器。

> 補圖

## 專案介紹及初步的設定

專案建立完成後，有了初始的專案資料夾，首先要來建立此專案中各個流程會使用到的資料夾及檔案，如下所示：

> 注意：我們會忽略專案中預設的部分資料夾

**專案目錄說明**

```text
├──node_module/       # JS 套件庫（JS Libraries）
├──public/            # Static file
├──src/               # 放我們撰寫的程式的資料夾
    ├──App.js         # 預設第一個頁面
    ├──index.js       # 預設 React 專案入口
├──package.json       # JS相依性紀錄檔
└──package-lock.json  # 檢驗套件版本
```

頁面設定頁面設定