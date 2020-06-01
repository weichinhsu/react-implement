# 2-2 Bootstrap 套版

> 本章節會沿用之前建立的 my-first-project 專案來說明，讀者也可以新建一個專案，若忘記如何建立專案可以參考 [1-1 建立第一個 React 專案](https://weichin.gitbook.io/react-implement/ch1-react-introduction/1-first-react-project)。

有寫過網頁的讀者一定有聽過 Bootstrap，它提供許多好用的元件，讓我們在開發時，可以省去許多設計元件的時間，對 HTML 和 CSS 不熟的讀者來說是一大福音，同時使用 Bootstrap 的優點還有可以很容易讓網站達到響應式（Responsive web design，通常縮寫為RWD）的要求。

所以本小節會依照不同的情境，跟大家說明如何 Bootstrap 套版與使用 React Bootstrap，來快速開發網站。

## 套用 Bootstrap 模板

當讀者已經有完整的模板，但想要套用 React 時，便可以選擇這種方式，此方式的優點是可以很快速的建立一個有介面的 React 專案，不需要額外設計頁面，只需要針對程式邏輯修改即可，但缺點是我們需要再專案中額外加入原本模板中的 CSS 樣式、jQuery 或是 Javascript 等程式，可能會讓專案過於龐大。

### 步驟一：選擇模板

本小節使用的模板是 [Start Bootstrap](https://startbootstrap.com/themes/) 的免費模板，所以請大家先進入網站，選擇一個自己喜歡的模板（請記得選擇有 Free 標籤的模板，Pro 是付費帳戶才能使用的噢！），把模板下載到本機上，並解壓縮。

本範例以 [Freelancer](https://startbootstrap.com/themes/freelancer/) 模板為例。

![bootstrap-0](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-0.png?raw=true)

> 本小節教大家套版的方式不限於使用 Bootstrap 的模板，也可以是任意的模版網站提供的模板，但需要注意的是，讀者在使用免費模板時，需要注意模板的 License，也盡量不使用來路不明的模板，別因為一時的方便，造成後續的麻煩。
>
> 除了本小節會使用的 [Start Bootstrap](https://startbootstrap.com/themes/) 模板網站，這邊也提供幾個不錯的免費模板網站讓大家有更多的選樣，請記得在使用前一樣要先了解模板的 License 噢！  
> [HTML5UP](https://html5up.net/)  
> [Freehtml5](https://freehtml5.co/)  
> [TEMPLATED](https://templated.co/)

### 步驟二：觀察模板的 index.html

打開模板的專案與之前建立的專案 my-first-project （讀者也可以新建一個專案，若忘記如何建立專案可以參考 [1-1 建立第一個 React 專案](https://weichin.gitbook.io/react-implement/ch1-react-introduction/1-first-react-project)）。

首先，我們要先觀察模板專案的 index.html 檔中引入了哪些檔案（只要觀察 index.html 的最前面及最後面）。

在模板的 index.html 的最上面，head 標籤中，找到 link 相關的標籤，並看到 href 屬性，如果**不是完整的一個網址**，就代表他是從專案中引入的檔案，如下圖兩個紅框的 href 屬性分別是`assets/img/favicon.ico`和`css/styles.css` ，表示一個是引入 `assets` 資料夾下的檔案，另一個是引入`css` 下的檔案。

![bootstrap-1](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-1.png?raw=true)

接著，看到模板的 index.html 的最下方引入 Javascript 的地方，一樣找到 script 標籤中 src 屬性不是完整網址的標籤，如下圖紅框處，分別是`assets`資料夾下的檔案和`js`資料夾下的檔案。

![bootstrap-2](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-2.png?raw=true)

{% hint style="warning" %}
link 標籤的 href 屬性與 script 標籤的 src 屬性，如果不是呈現完整的網址時，表示它是引入本地專案中的檔案，如果是網址的模式，表示它是取自網路上公開的資源。

兩者的差異在於使用本地的檔案會增加專案的大小，但是要使用時沒有太多的限制，如果是直接使用網路資源時，雖然不會佔用專案的空間，但使用的環境就一定要有網路或是網路速度要快，不然載入網頁時，可能會為了要讀取這些資源，而導致頁面跑不出來或跑很久。
{% endhint %}

### 步驟三：加入必要檔案

從上一個步驟的觀察，可以知道模板會使用到三個資料夾下的檔案，分別是`assets`、`css`與`js`資料夾，所以要把這三個資料夾加入 React 專案中 public 資料夾中，如下圖所示：

![bootstrap-3](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-3.png?raw=true)

### 步驟四：修改 React 專案中的 index.html

加入必要檔案後，開啟專案中 public 資料夾下的 index.html 檔，把剛剛放入專案的檔案引入，引入專案中的檔案時，要在路徑上加上`%PUBLIC_URL%`，這可以讓專案在部署後，可以讀取在public 資料夾下的檔案。

{% hint style="info" %}
**%PUBLIC\_URL% 說明**  
Notice the use of %PUBLIC\_URL% in the tags above. It will be replaced with the URL of the `public` folder during the build. Only files inside the `public` folder can be referenced from the HTML.
{% endhint %}

完成後的 head 如下圖，基本上是模板上有引入什麼，在 React 中的 index.html 就引入什麼：

![bootstrap-4](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-4.png?raw=true)

{% hint style="warning" %}
這邊請記得，剛剛在模板中看到的完整網址（包含 link 標籤的 href 屬性與 script 標籤的 src 屬性）也要引入。
{% endhint %}

最後，在 body 標籤內的最下方引入 script，如下圖，一樣剛剛在模板中看到的完整網址（script 標籤的 src 屬性）也要引入：

![bootstrap-5](https://github.com/weichinhsu/react-implement/blob/master/images/ch2/bootstrap-5.png?raw=true)

### 步驟五：分割模板的 index.html

完成必要檔案的引入後，接下來回到模板的 index.html 檔，在 body 標籤內可以看到原本模板的所有內容都塞在這裡面，但這對於一個網頁來講是很難維護且不容易閱讀，要找東西時會非常困難，所以這個步驟我們要把原本模板的內容拆解成不同的 component。

大部分的模板都會將一個一個區塊分好，以 [Freelancer](https://startbootstrap.com/themes/freelancer/) 這個模板為例，body 標籤中可以看到又分為 Navigation、Masthead、Portfolio Section 和 About Section 等多個區塊，我們只要依照頁面上已經分好的區塊一一地放入 React 專案中即可。

這邊以模板的 Navigation 區塊為例，回到我們的專案中，在 src 資料夾下新增一個 components 資料夾用來存放之後要建立的元件，接著在此資料夾中再新增 Navigation.js，並在檔案中建立一個 Navigation component，如下：

```javascript
import React, { Component } from 'react';

class Navigation extends Component {
 render() {
  return (
   <nav className="navbar navbar-expand-lg bg-secondary text-uppercase fixed-top" id="mainNav">
    <div className="container">
     <a className="navbar-brand js-scroll-trigger" href="#page-top">Start Bootstrap</a>
     <button className="navbar-toggler navbar-toggler-right text-uppercase font-weight-bold bg-primary text-white rounded"
      type="button" data-toggle="collapse" data-target="#navbarResponsive"
      aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
      Menu <i className="fas fa-bars"></i>
     </button>
     <div className="collapse navbar-collapse" id="navbarResponsive">
      <ul className="navbar-nav ml-auto">
       <li className="nav-item mx-0 mx-lg-1">
        <a className="nav-link py-3 px-0 px-lg-3 rounded js-scroll-trigger" href="#portfolio">Portfolio</a></li>
       <li className="nav-item mx-0 mx-lg-1">
        <a className="nav-link py-3 px-0 px-lg-3 rounded js-scroll-trigger" href="#about">About</a></li>
       <li className="nav-item mx-0 mx-lg-1">
        <a className="nav-link py-3 px-0 px-lg-3 rounded js-scroll-trigger" href="#contact">Contact</a></li>
      </ul>
     </div>
    </div>
   </nav>
  );
 }
}

export default Navigation;
```

**程式碼說明**

1. 第 3 行程式碼，建立一個 Navigation component。
2. 第 6-25 行程式碼，將模板上的 Navigation 區塊複製到 return 中貼上。
3. 第 30 行程式碼，將 Navigation component 匯出。

{% hint style="danger" %}
一般我們在 HTML 標籤上很常看到的 class 類別，在 React 中叫做 className，所以讀者在複製 HTML 到 React 的專案中時，請記得將 class 改為 className 噢！
{% endhint %}

再以 Masthead 區塊為例，一樣在 components 資料夾下建立 Masthead.js，如下所示：

```javascript
import React, { Component } from 'react';

class Masthead extends Component {
 render() {
  return (
   <header className="masthead bg-primary text-white text-center">
    <div className="container d-flex align-items-center flex-column">
     <img className="masthead-avatar mb-5" src="assets/img/avataaars.svg" alt="" />
     <h1 className="masthead-heading text-uppercase mb-0">Start Bootstrap</h1>
     <div className="divider-custom divider-light">
      <div className="divider-custom-line"></div>
      <div className="divider-custom-icon"><i className="fas fa-star"></i></div>
      <div className="divider-custom-line"></div>
     </div>
     <p className="masthead-subheading font-weight-light mb-0">Graphic Artist - Web Designer - Illustrator</p>
    </div>
   </header>
  );
 }
}

export default Masthead;
```

其他的區塊依此類推，在 components 資料夾下建立各區塊的元件，這邊就不再一一贅述。

### 步驟六：引入 Components

完成模板區塊的引入後，接下來回到 App.js 中，將這些 Component 引入， 如下所示：

```javascript
import React, { Component } from 'react';
import Navigation from './components/Navigation'
import Masthead from './components/Masthead'
import Portfolio from './components/Portfolio'
import About from './components/About'
import Contact from './components/Contact'
import Footer from './components/Footer'
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Navigation/>
        <Masthead/>
        <Portfolio/>
        <About/>
        <Contact/>
        <Footer/>
      </div>
    );
  }
}

export default App;
```

**程式碼說明**

1. 第 2-7 行程式碼，引入各元件。
2. 第 14-19 程式碼，將各元件加入 render 中。

完成上述的步驟後，就可以開啟終端機，進入專案目錄下執行 `npm start` 運行程式，並在瀏覽器上查看結果。

到這邊便已經完成在 React 專案套用 Bootstrap 模板囉！

### 步驟七：更新 GitHub

最後，我們要將套用 Bootstrap 模板的專案更新到在前一個小節的建立的 GitHub Repository 下，讓其他人也有看到讀者建立的網站。

所以開啟終端機，進入專案目錄下，依序輸入以下指令：

```javascript
git add .
git commit -m "use bootstrap template"
git push
```

完成更新後，便可以部署網頁至 GitHub Pages 上，指令如下：

```javascript
npm run deploy
```

發佈指令完成 published 後，便可以到之前 GitHub Pages 的網址瀏覽本章節建立 Bootstrap 模板的結果囉！

## React Bootstrap

如果讀者想要自己設計一個網頁，建議使用 React Bootstrap 來建立頁面，原因是 React Bootstrap 已經將原本 Bootstrap 提供的元件，轉換為 React 形式的 Component，所以使用起來會更貼近 React 的理念，以下開始教大家如何使用 React Bootstrap。

[React Bootstrap 官方網站](https://react-bootstrap.github.io/)

### 步驟一：安裝

首先，開啟終端機，輸入以下指令，進入專案中，並安裝 react-bootstrap 與 bootstrap 套件：

```text
cd my-first-project
npm install react-bootstrap bootstrap
```

### 步驟二：使用方式

安裝完成後，就可以在頁面上引入 React Bootstrap 提供的 Components，使用方式如下，在 App.js 檔案中，加入一個 Button Component：

```javascript
import React, { Component } from 'react';
import './App.css';
import { Button } from 'react-bootstrap';

class App extends Component {
  render() {
    const { isShow } = this.state
    return (
      <div className="App">
        <Button variant="primary">Primary</Button>
      </div>
    );
  }
}

export default App;
```

**程式碼說明**

1. 第 3 行程式碼，從 react-bootstrap 引入 Button 元件。
2. 第 10 行程式碼，在頁面上加入 Button 元件，並設定一些基本屬性。

> 元件屬性的設定方式可以到 React Bootstrap 官網上查詢。

從上述的範例，很快地就可以使用 react-bootstrap 的元件，而我們也可以從 React Bootstrap 的官網上查詢其他可以使用的元件、使用方式以及元件的屬性等。

[點擊查看 React Bootstrap 其他元件](https://react-bootstrap.github.io/components/alerts)

進入 React Bootstrap 官網後，點擊上方選單的「Components」按鈕，接著，在左側便可以看到所有提供的元件，如下圖所示，每個元件都有詳細的使用方式說明，因此讀者想要使用時，便可以直接過來這邊查詢即可！

