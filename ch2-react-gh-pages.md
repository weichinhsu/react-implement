# Ch3 使用 Github Pages 架設 React 專案

> 本章節會沿用之前建立的 my-first-project 專案。

本章節會教大家如何夠過 Github Pages 來架設一個屬於自己的網站。

在開始架設之前，有幾的本章節會使用的到知識，這邊跟大家稍微介紹一下，如果想更詳細了解的讀者可以點擊 Reference 進入維基查看更多。

**什麼是 Git？**

Git 是一個分散式版本控制軟體，很常被用來進行專案的版本控制。

[Reference: git Wikipedia](https://zh.wikipedia.org/wiki/Git)

**什麼是 GitHub？**

GitHub 是透過 Git 進行版本控制的**軟體原始碼代管服務平台**。

[Reference: GitHub Wikipedia](https://zh.wikipedia.org/wiki/GitHub)

**什麼是 GitHub Pages？**

GitHub Pages 是 GitHub 提供的一個網頁寄存服務，於2008年推出。可以**用於存放靜態網頁，包括博客、項目文檔甚至整本書**。

[Reference: GitHub Pages Wikipedia](https://zh.wikipedia.org/wiki/GitHub_Pages)

## 步驟一：建立 GitHub Repository

> 沒有 GitHub 帳號的讀者記得先去申請一個帳號，[點擊註冊 Github 帳號](https://github.com/join?return_to=%2Fweichinhsu%2Freact-implement&source=login)。

首先，登入 GitHub 後，來建立一個 Repository，如下圖，點擊右上角的圖像，並選擇「Your Repositories」。

![github-1](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-1.png?raw=true)

接著點擊右上角的「New」按鈕，來新增一個 Repository。

![github-2](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-2.png?raw=true)

設定 Repository

![github-3](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-3.png?raw=true)

**說明**

**紅框 1** 設定 Repository name ，這邊要特別注意 Repository name 是之後架設網站時的名稱，因此建議取一個適合網站的名稱。

例如這邊設定 Repository name 是 my-first-react，則發布網站後的網址則會是 `https://weichinhsu.github.io/my-first-react`，其中 weichinhsu 是筆者的 GitHub 帳號名稱，讀者們建立時會顯示自己的帳號名稱。

**紅框 2** 
由於之後需要將專案發佈，所以 Repository 必須設定 Public。如果想要設定 Private，但又要可以發布，則需要付費的帳戶。

**紅框 3** 
點擊「Create repository」建立專案。

## 步驟二：將專案放到 Github 上

> 此步驟會使用到 git 指令，因此請讀者先安裝 Git 的環境，[點擊進入 Git 官網安裝](https://git-scm.com/)。

建立好 Repository 後，我們要開始把專案放到 Github 上。首先打開終端機，進入專案中，並輸入指令建立 git。
```
cd my-first-project
git init
```

接著將專案的所有檔案加入要更新到 Github 項目中，指令如下：
```
git add .
```

加入完後，提交更新的項目，指令如下，其中`"first commit"`是讀者可以自行設定的資訊，可以當作是為此次專案更新所下的註解：
```
git commit -m "first commit"
```
將本地的專案與 Github 連結，指令如下，請注意這邊 remote 的位置資訊要改為讀者在前面所設定的 Repository 資訊：
```
git remote add origin git@github.com:weichinhsu/my-first-react.git
```
將專案上傳至 Github 上，指令如下：
```
git push -u origin master
```

完成後，再回到剛剛建立的 Github Repositor 頁面上，便可以看到專案囉！

![github-4](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-4.png?raw=true)

## 步驟一：安裝 Github Pages 套件
進入要架設網站的專案中，並安裝 gh-pages 
```
cd my-first-project
npm install --save-dgh-pages ev
```

