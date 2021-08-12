# 第一個 Redux 專案

本小節以一個簡單的留言板為範例，從介紹如何安裝Redux、專案環境到整個完整的Redux的流程，讓讀者可以更了解程式邏輯的運作過程。

> 本專案主要會以 Redux TypeScript 來說明，有時間的話也會寫一個 JavaScript 的版本ＸＤ

## 建立專案

首先開啟終端機，建立一個新的專案，我們使用官方已經定義好的redux-typescript template 來快速建立一個 Redux 專案，指令如下：
```
npx create-react-app my-redux-app --template redux-typescript
```
[Reference: redux-typescript template github](https://github.com/reduxjs/cra-template-redux-typescript)

建立完成後，輸入下列指令進入專案中，指令如下：
```
cd my-redux-app
```
接著透過npm，開始安裝一些我們之後會使用到的實用套件：
```
npm install react-router-dom
npm install antd
npm install history
```