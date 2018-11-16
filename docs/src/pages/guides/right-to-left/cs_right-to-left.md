# 右到左

<p class="description">要更改Material-UI組件的方向，您必須執行以下步驟。</p>

## 腳步

### 1。 HTML

確保在主體上設置了 `dir` 屬性，否則本機組件將中斷：

```html
<body dir="rtl">
```

### 2。 主題

在自定義主題中設置方向：

```js
const theme = createMuiTheme（{
  direction：'rtl'，
}）;
```

### 3。 JSS-RTL

你需要這個JSS插件來翻轉樣式： [jss-rtl](https://github.com/alitaheri/jss-rtl)。

```sh
npm install jss-rtl
```

在項目中安裝了插件後，Material-UI組件仍然需要由jss實例加載，如下所述。 在內部，當withStyles使用該JSS插件 `'RTL'：方向` 上設置的主題。

[CSS-in-JS文檔](/customization/css-in-js/#opting-out-of-rtl-transformation) 更多地解釋了這個插件的工作原理。 前往 [插件README](https://github.com/alitaheri/jss-rtl) 了解更多相關信息。

使用插件創建新的JSS實例後，需要使其可用於組件樹中的所有組件。 JSS有一個 [`JssProvider`](https://github.com/cssinjs/react-jss) 組件：

```jsx
從'jss'導入 { create } ;
從'jss-rtl'導入rtl;
從'react-jss / lib / JssProvider'導入JssProvider;
從'@ material-ui / core / styles'導入 { createGenerateClassName, jssPreset } ;

//配置JSS
const jss = create（{plugins：[... jssPreset（）。plugins，rtl（）]}）;

//自定義材質-UI類名生成器。
const generateClassName = createGenerateClassName（）;

功能RTL（道具）{
  返回（
    <JssProvider jss={jss} generateClassName={generateClassName}>
      {props.children}
    </JssProvider>
  ）;
}
```

## 演示

*使用右上角的方向切換按鈕翻轉整個文檔*

{{“demo”：“pages / guides / right-to-left / Direction.js”}}

## 選擇退出rtl轉型

如果您想阻止特定規則集受到 `rtl` 轉換的影響，您可以在開頭添加 `flip：false`：

*使用右上角的方向切換按鈕查看效果*

{{“demo”：“pages / guides / right-to-left / RtlOptOut.js”，“hideEditButton”：true}}