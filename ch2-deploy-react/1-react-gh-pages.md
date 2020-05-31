# 2-1 GitHub Pages

> 本章節會沿用之前建立的 my-first-project 專案。

本章節會教大家如何夠過 Github Pages 來架設一個屬於自己的網站。

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

**紅框 2** 由於之後需要將專案發佈，所以 Repository 必須設定 Public。如果想要設定 Private，但又要可以發布，則需要付費的帳戶。

**紅框 3** 點擊「Create repository」建立專案。

## 步驟二：將專案放到 Github 上

> 此步驟會使用到 git 指令，因此請讀者先安裝 Git 的環境，[點擊進入 Git 官網安裝](https://git-scm.com/)。

建立好 Repository 後，我們要開始把專案放到 Github 上。首先打開終端機，進入專案中，並輸入指令建立 git。

```text
cd my-first-project
git init
```

接著將專案的所有檔案加入要更新到 Github 項目中，指令如下：

```text
git add .
```

加入完後，提交更新的項目，指令如下，其中`"first commit"`是讀者可以自行設定的資訊，可以當作是為此次專案更新所下的註解：

```text
git commit -m "first commit"
```

將本地的專案與 Github 連結，指令如下：

> 請注意這邊 remote 的位置資訊要改為讀者在前面所設定的 Repository 資訊。

```text
git remote add origin git@github.com:weichinhsu/my-first-react.git
```

將專案上傳至 Github 上，指令如下：

```text
git push -u origin master
```

完成後，再回到剛剛建立的 Github Repository 頁面上，便可以看到專案囉！

![github-4](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-4.png?raw=true)

## 步驟三：安裝 Github Pages 套件

進入要架設網站的專案中，並安裝 gh-pages，如下：

```text
cd my-first-project
npm install --save-dgh-pages ev
```

> gh-pages github reference: [https://github.com/tschaub/gh-pages](https://github.com/tschaub/gh-pages)

## 步驟四：設定 package.json

開啟專案中的 package.json，設定 homepage 屬性，如下第三行。

> 請注意 homepage 的值需要設定成讀者在 Github 上的 Repository 位置。

```javascript
"name": "my-first-react",
"version": "0.1.0",
"homepage": "https://weichinhsu.github.io/my-first-react",
"private": true,
//...
```

{% hint style="info" %}
homepage 的格式為 `https://Github帳號名.github.io/Repository名稱`
{% endhint %}

接著同樣在 package.json 中，找到 scripts 區塊，並加上 predeploy 與 deploy 屬性，如下：

```javascript
"predeploy": "npm run build",
"deploy": "gh-pages -d build"
```

![&#x52A0;&#x4E0A; scripts](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-5.png?raw=true)

完成後，我們要將這次新增的設定，更新到 Github 上。所以一樣開啟終端機，在專案中依序輸入以下指令：

> 請記得也要在專案目錄下執行 git 指令噢！

```text
git add .
git commit -m "set gh-pages"
git push
```

接著輸入部署指令，將專案自動部署到 Github Pages 上：

```text
npm run deploy
```

## 步驟五：查看專案

完成部署後，開啟 Github Repository 專案的位置，點擊「Settings」按鈕。

![github-6](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-6.png?raw=true)

進入 Setting，往下滑就可以看到 Github Pages 的區塊，如下圖，網頁上會告訴你，專案的已經發佈，`Your site is published at https://weichinhsu.github.io/my-first-react/`，點擊網址後，就可以看到自己的網頁囉！

> 下圖只是示意圖，因此網址會是前面在 package.json 上設定的 homepage 路徑。

![github-7](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/github-7.png?raw=true)

{% hint style="warning" %}
執行 `npm run deploy` 部署網頁後，如果進入 Github Pages 時是顯示 404 Not found 的頁面時，請等待幾分鐘的時間完成發布。
{% endhint %}

{% hint style="info" %}
如果這篇文章對你有幫助，可以前往 [Github react-implement](https://github.com/weichinhsu/react-implement) 按下 Star 來支持我，我會不定期的更新教學內容。 也可以 follow 我的 Github 帳號，未來我也會繼續寫更多的網頁技術與大家分享！
{% endhint %}

