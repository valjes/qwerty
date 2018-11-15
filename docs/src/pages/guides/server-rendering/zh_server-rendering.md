# 服務器渲染

<p class="description">服務器端呈現的最常見用例是在用戶（或搜索引擎爬蟲）首次請求您的應用時處理初始呈現。</p>

當服務器收到請求時，它會將所需組件呈現為HTML字符串，然後將其作為響應發送給客戶端。 從那時起，客戶接管渲染職責。

## 服務器上的Material-UI

Material-UI是從頭開始設計的，具有在服務器上呈現的約束，但是由您決定是否正確集成。 為頁面提供所需的CSS非常重要，否則頁面將僅使用HTML呈現，然後等待客戶端注入CSS，導致其閃爍。 要將樣式註入客戶端，我們需要：

1. 在每個請求上創建一個全新的 `sheetRegistry` 和 `主題` 實例。
2. 使用服務器端API和實例呈現React樹。
3. 將CSS拉出 `sheetRegistry`。
4. 將CSS傳遞給客戶端。

在客戶端，CSS將在刪除服務器端注入的CSS之前第二次注入。

## 配置

在下面的配方中，我們將了解如何設置服務器端呈現。

### 服務器端

以下是我們的服務器端將會是什麼樣子的大綱。 我們將使用 [app.use](http://expressjs.com/en/api.html) 設置一個 [Express中間件](http://expressjs.com/en/guide/using-middleware.html) 來處理進入我們服務器的所有請求。 如果您不熟悉Express或中間件，只需知道每次服務器收到請求時都會調用我們的handleRender函數。

`server.js`

```js
從'快遞'進口快遞;
import來自'react'的React;
從'./App'導入應用程序;

//我們將在接下來的章節中填寫這些內容。
函數renderFullPage（html，css）{
  / * ... * /
}

函數handleRender（req，res）{
  / * ... * /
}

const app = express（）;

//每次服務器端收到請求時都會觸發此操作。
app.use（handleRender）;

const port = 3000;
app.listen（port）;
```

### 處理請求

我們需要對每個請求做的第一件事是創建一個新的 `sheetRegistry` 和 `主題` 實例。

渲染時，我們將 `App`，我們的根組件 包含在 `JssProvider` 和 [`MuiThemeProvider`](/api/mui-theme-provider/) 以使 `sheetRegistry` 和 `主題` 可用於組件樹中的所有組件。

在服務器端渲染的關鍵步驟，是為了使我們的組件的初始HTML **前** 我們把它發送給客戶端。 為此，我們使用 [ReactDOMServer.renderToString（）](https://reactjs.org/docs/react-dom-server.html)。

然後我們使用 `sheetRegistry.toString（）`從我們的 `sheetRegistry` 獲取CSS。 我們將在 `renderFullPage` 函數中看到它是如何傳遞的。

```jsx
從'react-dom / server'導入ReactDOMServer
從'jss'導入 { SheetsRegistry } ;
從'react-jss / lib / JssProvider'導入JssProvider;
從'@ material-ui / core / styles'導入{
  MuiThemeProvider，
  createMuiTheme，
  createGenerateClassName，
};
從'@ material-ui / core / colors / green'導入綠色;
從'@ material-ui / core / colors / red'導入紅色;

函數handleRender（req，res）{
  //創建一個sheetRegistry實例。
  const sheetsRegistry = new SheetsRegistry（）;

  //創建sheetManager實例。
  const sheetsManager = new Map（）;

  //創建主題實例。
  const theme = createMuiTheme（{
    palette：{
      primary：green，
      accent：red，
      type：'light'，
    }，
  }）;

  //創建一個新的類名生成器。
  const generateClassName = createGenerateClassName（）;

  //將組件渲染為字符串。
  const html = ReactDOMServer.renderToString（
    <JssProvider registry={sheetsRegistry} generateClassName={generateClassName}>
      <MuiThemeProvider theme={theme} sheetsManager={sheetsManager}>
        <App />
      </MuiThemeProvider>
    </JssProvider>
  ）

  //從我們的sheetsRegistry中獲取CSS。
  const css = sheetsRegistry.toString（）

  //將呈現的頁面發送回客戶端。
  res.send（renderFullPage（html，css））
}
```

### 注入初始組件HTML和CSS

服務器端的最後一步是將我們的初始組件HTML和CSS注入到要在客戶端呈現的模板中。

```js
功能renderFullPage（HTML，CSS）{
  返回`
    <！DOCTYPE HTML>
    <html>
      <head>
        <title>材料的UI</title>
      </head>
      <body>
        <div id="root">${html}</div>
        <style id="jss-server-side">${css}</style>
      </body>
    </html>
  `;
}
```

### 客戶端

客戶端很簡單。 我們需要做的就是刪除服務器端生成的CSS。 我們來看看我們的客戶端文件：

`client.js`

```jsx
從'react'中導入React;
從'react-dom'導入ReactDOM;
從'react-jss / lib / JssProvider'導入JssProvider;
從'@ material-ui / core / styles'導入{
  MuiThemeProvider，
  createMuiTheme，
  createGenerateClassName，
};
從'@ material-ui / core / colors / green'導入綠色;
從'@ material-ui / core / colors / red'導入紅色;
從'./App'導入應用程序;

類Main擴展React.Component {
  //刪除服務器端注入的CSS。
  componentDidMount（）{
    const jssStyles = document.getElementById（'jss-server-side'）;
    if（jssStyles && jssStyles.parentNode）{
      jssStyles.parentNode.removeChild（jssStyles）;
    }
  }

  render（）{
    return <App />
  }
}

//創建一個主題實例。
const theme = createMuiTheme（{
  palette：{
    primary：green，
    accent：red，
    type：'light'，
  }，
}）;

//創建一個新的類名生成器。
const generateClassName = createGenerateClassName（）;

ReactDOM.hydrate（
  <JssProvider generateClassName={generateClassName}>
    <MuiThemeProvider theme={theme}>
      <Main />
    </MuiThemeProvider>
  </JssProvider>，
  document.querySelector（'＃根'），
）;
```

## 參考實現

我們託管不同的參考實現，您可以在 [`/ examples`](https://github.com/mui-org/material-ui/tree/master/examples) 文件夾下的 [GitHub存儲庫](https://github.com/mui-org/material-ui) 找到它們：

- [本教程的參考實現](https://github.com/mui-org/material-ui/tree/master/examples/ssr)
- [Next.js](https://github.com/mui-org/material-ui/tree/master/examples/nextjs)
- [蓋茨比](https://github.com/mui-org/material-ui/tree/master/examples/gatsby)

## 故障排除

如果它不起作用，在99％的情況下，這是一個配置問題。 缺少的屬性，錯誤的調用順序或缺少的組件。 我們對配置非常嚴格，找出錯誤的最佳方法是將項目與已經正常工作的設置進行比較，一點一點地查看我們的 [參考實現](#reference-implementations)。

### CSS僅在第一次加載時起作用然後丟失

CSS僅在頁面的第一次加載時生成。 然後，服務器上缺少連續請求的CSS。

#### 要採取的行動

我們依賴緩存（工作表管理器），每個組件類型 只注入一次CSS（如果你使用兩個按鈕，你只需要一次按鈕的CSS）。 您需要為每個請求</strong>提供 **個新的 `圖紙管理器`。</p> 

您可以了解更多關於 [的文檔中的張經理概念](/customization/css-in-js/#sheets-manager)。

*修復示例：*

```diff
-  //創建一個sheetManager實例。
-const sheetsManager = new Map（）;

函數handleRender（req，res）{

+ //創建一個sheetManager實例。
+ const sheetsManager = new Map（）;

  // ...

  //將組件渲染為字符串。
  const html = ReactDOMServer.renderToString（
```

### 反應類名稱水合不匹配

客戶端和服務器之間存在類名不匹配。 它可能適用於第一個請求。 另一個症狀是樣式在初始頁面加載和客戶端腳本下載之間發生變化。

#### 要採取的行動

類名值依賴於 [類名生成器](/customization/css-in-js/#creategenerateclassname-options-class-name-generator)的概念。 整個頁面需要用 **單個生成器**渲染。 此生成器需要在服務器和客戶端上具有相同的行為。 例如：

- 您需要為每個請求提供一個新的類名生成器。 但是您可以在不同的請求之間共享 `createGenerateClassName（）`：

*修復示例：*

```diff
-  //創建一個新的類名生成器。
-const generateClassName = createGenerateClassName（）;

函數handleRender（req，res）{

+ //創建一個新的類名生成器。
+ const generateClassName = createGenerateClassName（）;

  // ...

  //將組件渲染為字符串。
  const html = ReactDOMServer.renderToString（
```

- 您需要驗證您的客戶端和服務器是否正在運行 **與Material-UI完全相同的版本**。 即使是次要版本的不匹配也可能導致樣式問題。 要檢查版本號，請在構建應用程序的環境中以及部署環境中運行 `npm list @ material-ui / core`。
    
    您還可以通過在package.json的依賴項中指定特定的MUI版本來確保不同環境中的相同版本。

*fix（package.json）的示例：*

```diff
  “依賴”：{
...

- “@ material-ui / core”：“^ 1.4.2”，
+“@ material-ui / core”：“1.4.3”，
...
  },
```

- 您需要確保服務器和客戶端共享相同的 `process.env.NODE_ENV` 值。