# 2-2 Bootstrap

> 本章節會沿用之前建立的 my-first-project 專案。

有寫過網頁的讀者一定有聽過 Bootstrap，它提供許多好用的元件，讓我們在開發時，可以省去許多設計元件的時間，對 HTML 和 CSS 不熟的讀者來說是一大福音，同時使用 Bootstrap 的優點還有可以很容易讓網站達到響應式（Responsive web design，通常縮寫為RWD）的要求。

所以本小節會依照不同的情境，跟大家說明如何 Bootstrap 套版與使用 React Bootstrap，來快速開發網站。

## 套用 Bootstrap 模板

當讀者已經有完整的模板，但想要套用 React 時，便可以選擇這種方式，此方式的優點是可以很快速的建立一個有介面的 React 專案，不需要額外設計頁面，只需要針對程式邏輯修改即可，但缺點是我們需要再專案中額外加入原本模板中的 CSS 樣式、jQuery 或是 Javascript 等程式，可能會讓專案過於龐大。

### 步驟一：選擇模板

本小節使用的模板是 [Start Bootstrap](https://startbootstrap.com/themes/) 的免費模板，所以請大家先進入網站，選擇一個自己喜歡的模板（請記得選擇有 Free 標籤的模板，Pro 是付費帳戶才能使用的噢！），把模板下載到本機上，並解壓縮。

> 此方式不限於使用 Bootstrap 的模板，也可以是任意的模版網站提供的模板，但需要注意的是，讀者在使用免費模板時，需要注意模板的 License，也盡量不使用來路不明的模板，別因為一時的方便，造成後續的麻煩。
>
> 除了本小節會使用的 [Start Bootstrap](https://startbootstrap.com/themes/) 模板網站，這邊也提供幾個不錯的免費模板網站讓大家有更多的選樣，請記得在使用前一樣要先了解模板的 License 噢！  
> [HTML5UP](https://html5up.net/)  
> [Freehtml5](https://freehtml5.co/)  
> [TEMPLATED](https://templated.co/)

### 步驟二：觀察模板的 index.html

打開模板的專案與之前建立的專案 my-first-project （讀者也可以新建一個專案），首先，我們要先觀察模板專案的 index.html 檔中引入了哪些檔案（只要觀察 index.html 的最前面及最後面）。

在模板的 index.html 的最上面，head 標籤中，找到 link 相關的標籤，並看到 href 屬性，如果不是完整的一個網址，就代表他是從專案中引入的檔案，如下圖兩個紅框的 href 屬性分別是`assets/img/favicon.ico`和`css/styles.css` ，表示一個是引入 `assets` 資料夾下的檔案，另一個是引入`css` 下的檔案。

![bootstrap-1](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-1.png?raw=true)

接著，看到模板的 index.html 的最下方引入 Javascript 的地方，一樣找到 script 標籤中 src 屬性不是完整網址的標籤，如下圖紅框處，分別是`assets`資料夾下的檔案和`js`資料夾下的檔案。

![bootstrap-2](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-2.png?raw=true)

### 步驟三：匯入必要檔案

從上一個步驟的觀察，可以知道會使用到三個資料夾下的檔案，分別是`assets`、`css`與`js`資料夾，所以要把這三個資料夾加入 React 專案中 public 資料夾中，如下圖所示：

![bootstrap-2](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-2.png?raw=true)

### 步驟四：修改 React 專案中的 index.html

### 步驟五：分割模板的 index.html

### 步驟六：引入 Components

### 步驟七：更新 GitHub 

