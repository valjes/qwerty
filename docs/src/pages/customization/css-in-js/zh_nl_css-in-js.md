# JS中的CSS

<p class="description">即使您不使用我們的組件，您也可以利用我們的樣式解決方案。</p>

Material-UI旨在為構建動態UI提供堅實的基礎。 為簡單起見，起見 **我們暴露我們的造型解決方案，用戶**。 你可以使用它，但你不必這樣做。 這種造型的解決方案是 [與互操作](/guides/interoperability/) 所有其他主要的解決方案。

## Material-UI的造型解決方案

在以前的版本中，Material-UI使用了LESS，然後使用自定義內聯式解決方案來編寫組件的樣式，但這些方法已被證明是有限的。 最近，我們將 [轉向](https://github.com/oliviertassinari/a-journey-toward-better-style) a *CSS-in-JS* 解決方案。 它 **解鎖許多強大的功能** （主題嵌套，動態模式，自我支持等）。 我們認為這是未來：

- [統一的樣式語言](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660)
- [基於組件的樣式的未來](https://medium.freecodecamp.org/css-in-javascript-the-future-of-component-based-styling-70b161a79a32)
- [將SCSS（Sass）轉換為CSS-in-JS](https://egghead.io/courses/convert-scss-sass-to-css-in-js)

所以，您可能已經在演示中註意到了 *CSS-in-JS* 樣子。 我們使用由 [`withStyles`](#api) 創建的高階組件，使用JSS將一組樣式作為CSS注入到DOM中。 這是一個例子：

{{“demo”：“pages / customization / css-in-js / CssInJs.js”}}

## JSS

Material-UI的樣式解決方案使用 [JSS](https://github.com/cssinjs/jss) 作為核心。 它是一個 [高性能](https://github.com/cssinjs/jss/blob/master/docs/performance.md) JS到CSS編譯器，它在運行時和服務器端工作。 它大約是8 kB（縮小和壓縮），並且可以通過 [插件](https://github.com/cssinjs/jss/blob/master/docs/plugins.md) API進行擴展。

如果你最終使用的代碼庫這種樣式的解決方案，你將需要 *學會API*。 最好的起點是查看每個 [插件](http://cssinjs.org/plugins/) 提供的功能。 Material-UI使用其中 [](#plugins)。 如果需要，您可以隨時使用 [`JssProvider`](https://github.com/cssinjs/react-jss#custom-setup) 幫助程序添加新插件。

如果你想建立你自己的 `jss` **和** 支持 *rtl* 的實例，請確保你還包括 [jss-rtl](https://github.com/alitaheri/jss-rtl) 插件。 檢查jss-rtl [自述文件](https://github.com/alitaheri/jss-rtl#simple-usage) 以了解具體方法。

## 表格註冊表

在服務器上渲染時，您需要將所有渲染樣式作為CSS字符串。 `SheetsRegistry` 類允許您手動聚合和字符串化它們。 閱讀有關 [Server Rendering](/guides/server-rendering/)更多信息。

{{“demo”：“pages / customization / css-in-js / JssRegistry.js”，“hideEditButton”：true}}

## 表格經理

工作表管理器使用 [引用計數](https://en.wikipedia.org/wiki/Reference_counting) 算法，以便每個（樣式，主題）對只附加和分離樣式表一次。 在重新渲染組件的實例時，此技術可提供重要的性能提升。

當只在客戶端上呈現時，這不是您需要注意的事情。 但是，在服務器上進行渲染時。 您可以閱讀有關 [Server Rendering](/guides/server-rendering/)更多信息。

## 班級名稱

您可能已經註意到我們的樣式解決方案生成的類名稱為 **非確定性**，因此您不能依賴它們保持不變。 以下CSS不起作用：

```css
.MuiAppBar-root-12 {
  opacity: 0.6
}
```

相反，您必須使用組件的 `類` 屬性來覆蓋它們。 另一方面，由於我們的類名稱的非確定性，我們可以實現開發和生產的優化。 它們易於在開發中進行調試，並且在生產中盡可能短：

- 開發： `.MuiAppBar-root-12`
- 產量： `.jss12`

如果您不喜歡此默認行為，則可以更改它。 JSS依賴於 [類名生成器](http://cssinjs.org/js-api/#generate-your-own-class-names)的概念。

### 全球CSS

我們為Material-UI需求提供了類名生成器的自定義實現： [`createGenerateClassName（）`](#creategenerateclassname-options-class-name-generator)。 以及使用 `dangerouslyUseGlobalCSS` 選項使類名為 **deterministic** 的選項。 打開時，類名稱將如下所示：

- 開發： `.MuiAppBar-root`
- 製作： `.MuiAppBar-root`

⚠️ **使用時要謹慎 `dangerouslyUseGlobalCSS`。** 我們提供此選項作為快速原型製作的逃生艙口。 依賴它來生成在生產中運行的代碼具有以下含義：

- 全局CSS本質上是脆弱的。 人們使用嚴格的方法，如 [BEM](http://getbem.com/introduction/) 來解決問題。
- 跟踪 `類` API變化更難。

⚠️當使用 `dangerouslyUseGlobalCSS` 獨立（沒有Material-UI）時，您應該命名樣式表。 `withStyles` 有一個名稱選項：

```jsx
const Button = withStyles（styles， { name: 'button' }）（ButtonBase）
```

## CSS注入順序

由Material-UI注入的用於樣式化組件的CSS具有最高的特異性，因為 `<link>` 被注入到 `<head>` 的底部，以確保組件始終正確呈現。

但是，您可能還希望覆蓋這些樣式，例如使用樣式化組件。 如果您遇到CSS注入訂單問題，JSS [提供了一種機制](https://github.com/cssinjs/jss/blob/master/docs/setup.md#specify-dom-insertion-point) 來處理這種情況。 通過調整安置 `insertionPoint` 你的HTML頭內可以 [控制命令](http://cssinjs.org/js-api/#attach-style-sheets-in-a-specific-order) 的CSS規則應用到您的組件。

### HTML評論

最簡單的方法是添加一個HTML註釋，確定JSS將注入樣式的位置：

```jsx
<head>
  <！ -  jss-insertion-point  ->
  <link href="..." />
</head>
```

```jsx
從'react-jss / lib / JssProvider'導入JssProvider;
從'jss'導入 { create } ;
從'@ material-ui / core / styles'導入 { createGenerateClassName, jssPreset } ;

const generateClassName = createGenerateClassName（）;
const jss = create（{
  ... jssPreset（），
  //我們定義一個自定義插入點，JSS將尋找在DOM中註入樣式。
  insertionPoint：'jss-insertion-point'，
}）;

功能App（）{
  return（
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  ）;
}

導出默認App;
```

### 其他HTML元素

[創建React應用程序](https://github.com/facebook/create-react-app) 在創建生成構建時刪除HTML註釋。 要解決此問題，您可以提供DOM元素（註釋除外）作為JSS插入點。

例如，一個 `<noscript>` 元素：

```jsx
<head>
  <noscript id="jss-insertion-point"></noscript>
  <link href="..." />
</head>
```

```jsx
從'react-jss / lib / JssProvider'導入JssProvider;
從'jss'導入 { create } ;
從'@ material-ui / core / styles'導入 { createGenerateClassName, jssPreset } ;

const generateClassName = createGenerateClassName（）;
const jss = create（{
  ... jssPreset（），
  //我們定義一個自定義插入點，JSS將尋找在DOM中註入樣式。
  insertionPoint：document.getElementById（'jss-insertion-point'），
}）;

功能App（）{
  return（
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  ）;
}

導出默認App;
```

### JS createComment

codesandbox.io阻止訪問 `<head>` 元素。 要解決此問題，您可以使用JavaScript `document.createComment（）` API：

```jsx
從'react-jss / lib / JssProvider'導入JssProvider;
從'jss'導入 { create } ;
從'@ material-ui / core / styles'導入 { createGenerateClassName, jssPreset } ;

const styleNode = document.createComment（“jss-insertion-point”）;
document.head.insertBefore（styleNode，document.head.firstChild）;

const generateClassName = createGenerateClassName（）;
const jss = create（{
  ... jssPreset（），
  //我們定義一個自定義插入點，JSS將尋找在DOM中註入樣式。
  insertionPoint：'jss-insertion-point'，
}）;

功能App（）{
  return（
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  ）;
}

導出默認App;
```

## JssProvider

react-jss公開了一個 `JssProvider` 組件，為底層子組件配置JSS。 有不同的用例：

- 提供類名生成器。
- [提供表格註冊表。](/customization/css-in-js/#sheets-registry)
- 提供JSS實例。 您可能希望支持 [從右到左](/guides/right-to-left/) 或更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)。 閱讀 [的JSS文件](http://cssinjs.org/js-api/) ，詳細了解可用的選項。 這是一個例子：

```jsx
從'react-jss / lib / JssProvider'導入JssProvider;
從'jss'導入 { create } ;
從'@ material-ui / core / styles'導入 { createGenerateClassName, jssPreset } ;

const generateClassName = createGenerateClassName（）;
const jss = create（jssPreset（））;

功能App（）{
  返回（
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  ）;
}

導出默認App;
```

## 插件

JSS使用插件的概念來擴展其核心，允許人們挑選他們需要的功能。 您僅為您正在使用的內容支付性能開銷。 給定 `withStyles` 是我們的內部樣式解決方案，默認情況下所有插件都不可用。 我們添加了以下列表：

- [JSS-全球](http://cssinjs.org/jss-global/)
- [JSS-嵌套](http://cssinjs.org/jss-nested/)
- [JSS-駝峰](http://cssinjs.org/jss-camel-case/)
- [JSS-默認單元](http://cssinjs.org/jss-default-unit/)
- [JSS-廠商prefixer](http://cssinjs.org/jss-vendor-prefixer/)
- [JSS-道具排序](http://cssinjs.org/jss-props-sort/)

它是 [jss-preset-default](http://cssinjs.org/jss-preset-default/)的子集。 當然，您可以自由添加新插件。 我們有一個 [`jss-rtl` 插件](/guides/right-to-left/#3-jss-rtl)例子。

## API

### `withStyles（styles， [options]）=> 個高階分量`

將樣式表與組件鏈接。 它不會修改傳遞給它的組件;相反，它返回一個 `類` 屬性的新組件。 這個 `類` 對象包含DOM中註入的類名的名稱。

一些可能有趣的實現細節：

- 它添加了 `類` 屬性，因此您可以從外部覆蓋注入的類名。
- 它添加了一個 `innerRef` 屬性，因此您可以獲得對包裝組件的引用。 `innerRef` 的使用與 `ref`相同。
- 它轉發 *非React靜態* 屬性，因此這個HOC更“透明”。 例如，它可以用於定義一個 `getInitialProps（）` 靜態方法（next.js）。

#### 參數

1. `樣式` （*函數|對象*）：生成樣式或樣式對象的函數。 它將鏈接到組件。 如果您需要訪問主題，請使用函數簽名。 它是作為第一個參數提供的。
2. `選項` （*對象* [optional]）： 
    - `options.withTheme` （*布爾值* [optional]）：默認值為 `false`。 將 `主題` 對像作為屬性提供給組件。
    - `options.name` （*String* [optional]）：樣式表的名稱。 用於調試。 如果未提供該值，它將嘗試回退到組件的名稱。
    - `options.flip` （*布爾值* [optional]）：當設置為 `false`，此工作表將選擇退出 `rtl` 轉換。 設置為 `true`，樣式將反轉。 設置為 `null`，它遵循 `theme.direction`。
    - 其它鍵被轉發到的選項參數 [jss.createStyleSheet（[styles]， [options]）](http://cssinjs.org/js-api/#create-style-sheet)。

#### 返回

`高階組件`：應該用於包裝組件。

#### 例子

```jsx
從'@ material-ui / core / styles'導入 { withStyles } ;

const的樣式= {
  根： {
    backgroundColor: 'red',
  }，
};

類MyComponent擴展了React.Component {
  render（）{
    return <div className={this.props.classes.root} />;
  }
}

導出默認值withStyles（樣式）（MyComponent）;
```

此外，您可以使用 [裝飾器](https://babeljs.io/docs/en/babel-plugin-proposal-decorators) 如下所示：

```jsx
從'@ material-ui / core / styles'導入 { withStyles } ;

const的樣式= {
  根： {
    backgroundColor: 'red',
  }，
};

@withStyles（styles）
類MyComponent擴展React.Component {
  render（）{
    return <div className={this.props.classes.root} />;
  }
}

導出默認MyComponent
```

### `createGenerateClassName（[options]）=> 類名生成器`

返回 [類名生成器函數](http://cssinjs.org/js-api/#generate-your-own-class-names)函數。

#### 參數

1. `選項` （*對象* [optional]）： 
    - `options.dangerouslyUseGlobalCSS` （*布爾值* [optional]）：默認值為 `false`。 使Material-UI類名稱具有確定性。
    - `options.productionPrefix` （*字符串* [optional]）：默認為 `'JSS'`。 用於在生產中為類名添加前綴的字符串。
    - `options.seed` （*字符串* [optional]）：默認為 `''`。 用於唯一標識生成器的字符串。 當使用多個生成器時，它可用於避免類名衝突。

#### 返回

`類名生成器`：應該向JSS提供生成器。

#### 例子

```jsx
從'react-jss / lib / JssProvider'導入JssProvider;
從'@ material-ui / core / styles'導入 { createGenerateClassName } ;

const generateClassName = createGenerateClassName（{
  dangerouslyUseGlobalCSS：true，
  productionPrefix：'c'，
}）;

功能App（）{
  返回（
    <JssProvider generateClassName={generateClassName}>
...
    </JssProvider>
  ）;
}

導出默認App;
```

## 替代API

你認為 [個高階組件是新的mixins](https://cdb.reacttraining.com/use-a-render-prop-50de598f11ce)嗎？ 請放心，我們不會這樣做，但是因為 `withStyles（）` 是一個高階組件，所以只需要 **行代碼** 就可以擴展它，以匹配所有慣用的React模式。 這裡有幾個例子。

### 渲染道具API（+11行）

術語 [“渲染道具”](https://reactjs.org/docs/render-props.html) 指的是使用其值為函數的道具在React組件之間共享代碼的簡單技術。

```jsx
//您將在演示源中找到`createStyled`實現。
常量樣式化= createStyled（{
  根：{
    背景：'線性梯度（45deg，＃FE6B8B 30％，＃FF8E53 90％）'，
    borderRadius：3，
    邊界：0，
    色：“白色”，
    高度：48，
    填充：'0 30PX'，
    boxShadow：'0 3PX 5px的2px的RGBA（255，105，135，0.3）'，
  }，
}）;

函數RenderProps（）{
  return（
    <Styled>
      {（{ classes }）=> （
        <Button className={classes.root}>
          {'Render props'}
        </Button>
      ）}
    </Styled>
  ）;
}
```

{{“demo”：“pages / customization / css-in-js / RenderProps.js”}}

您可以像使用 `withStyles`一樣訪問主題：

```js
常量樣式化= createStyled（主題=> （{
  根： {
    backgroundColor: theme.palette.background.paper,
  }，
}））;
```

[@ jedwards1211](https://github.com/jedwards1211) 花時間將此模塊移動到一個包中： [material-ui-render-props-styles](https://github.com/jcoreio/material-ui-render-props-styles)。 隨意使用它。

### 樣式組件API（+15行）

styled-components的API刪除了組件和样式之間的映射。 使用組件作為低級樣式構造可以更簡單。

```jsx
//您將在演示源中找到`styled`實現。
//你甚至可以用https://github.com/cssinjs/jss-template編寫CSS。
常量為myButton =樣式（按鈕）（{
  背景：'線性梯度（45deg，＃FE6B8B 30％，＃FF8E53 90％）'，
  borderRadius：3，
  邊界：0，
  色：“白色”，
  高度：48，
  填充：'0 30PX'，
  boxShadow：'0 3PX 5px的2px的RGBA（255，105，135，0.3）'，
}）;

函數StyledComponents（）{
  return <MyButton>{'Styled Components'}</MyButton>;
}
```

{{“demo”：“pages / customization / css-in-js / StyledComponents.js”}}

您可以像使用 `withStyles`一樣訪問主題：

```js
const MyButton = styled（Button）（theme => （{
  backgroundColor：theme.palette.background.paper，
}））;
```