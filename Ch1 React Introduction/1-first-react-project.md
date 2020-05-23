# 建立第一個 React 專案

本章節開始教導讀者如何建立一個 React 專案，以及如何在瀏覽器上運行專案。

## 1. 建立專案
**1. 使用 npx 指令建立第一個 React 專案**
```
npx create-react-app my-first-project
```
**指令說明** <br>
上述指令表示透過 npx 去執行 create-react-app 指令，來建立 React 專案，並命名為 my-first-project 。

**2. 進入專案**
```
cd my-first-project
```
**指令說明** <br>
透過 cd 指令進入專案中。

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