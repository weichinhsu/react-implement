# Chapter 2 Redux 介紹
經過前面章節後，相信讀者對 React 有一定程度的熟悉了，因此本章節便要開始加入 Redux 的概念，將程式依照不同的工作性質分工，不再是把所有的邏輯通通寫在同一個頁面上，造成可讀性下降，而在維護程式時，也能夠快速地找到問題所在。本章節包含介紹Redux的由來、基礎觀念、安裝環境以及最後會以範例帶領讀者一步一步建立Redux專案。

## 什麼是Redux
Redux是一個函式庫，由 Flux 概念所衍伸而來，目的是實作出簡單又易操作的程式框架，由於在一個 React 的應用程式中，state 是不可或缺的部分，不管是在頁面上記錄的狀態，或是不同組件，甚至不同頁面中互相傳遞的狀態，因此當應用程式越來越大，頁面上的組件或需要處理的邏輯程式也越來越多時，便會造成 state 過於複雜，且難以管理，這時候便可以透過 Redux 來簡化這些複雜的工作。

### Redux的由來
在介紹Redux之前，先讓我們來了解Flux的觀念及基本運作方式，接著會說明Redux是如何繼承Flux的理念，並實作出易操作的框架。

**Flux的運作方式**

Flux是一個單向資料流的概念，為了保護資料，它規定要存取資料時只能透過發送一個Action（動作）觸發，因此我們不需擔心資料會不會無故遭到更動，除非發送Action；而一個資料可能會需要讓多個頁面存取或是要長時間保留，所以Flux便提出了Store的概念，將此類的資料集中管理，若要修改儲存在Store的資料，則要透過前面提到的Action去進行更新的動作。

為了讓讀者可以更了解單向資料流的概念，我們以下圖來說明，可以看到圖中各個流程的箭頭都是單一方向，這便是Flux的單一資料流，表示資料傳送出去後，會走訪完整個流程後才回到頁面上，不會在兩個流程之間反覆的傳遞。而概念簡單來說，當在View（頁面）上要修改儲存在Store的資料時，便可以傳送Action到Dispatcher（發送器），其中Dispatcher可以想成是一個發送中心，接收各個不同頁面的Action所傳遞的資料來更新Store，最後便會重新渲染有取用Store的View。

![](https://i.imgur.com/S7XKt6I.png)

以新增待辦清單例子來說，當使用者在頁面（View）上輸入待辦項目，按下確認按鈕後，便會發送一個新增項目的Action到Dispatcher，而Dispatcher接收到後，便會去更新儲存在Store中的資料，最後會重新渲染頁面，將新增待辦事項顯示在頁面上。

**Redux的運作方式**

為了管理在React Native中變化不斷的state，Redux實作出Flux的概念，簡化程式的複雜度，理念大致上都與Flux相同，一樣都是單向資料流的運作方式，並新增了Reducer的概念，用來管理儲存在Store中的資料。

為了讓讀者更清楚地了解，以下圖來說明，可以看到在View觸發更新儲存在Store的State資料事件時，會傳送一個請求到Action Creator進行資料的處理並建立一個UPDATE action，接著將action發送到Reducer找到儲存在Store中正確的State值更新，最後便會重新渲染有取用Store的View，讓所有Hello更新為你好，這邊值得注意的是，Store的資料在View中是以Props的方式取得，表示是不能在頁面中隨意更動的值，必須透過發送完整的Redux流程才能更新。

![](https://i.imgur.com/LyWD47d.png)

這邊同樣以新增待辦清單例子來說，當使用者在頁面（View）上輸入待辦項目，按下確認按鈕後，便會發送一個新增待辦項目的請求到Action Creator步驟，將資料進行處理，完成後會建立一個新增待辦事項action，並進入Reducer步驟，將資料存入Store中，最後會重新渲染頁面，將新增待辦事項顯示在頁面上。




