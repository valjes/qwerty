# 安裝

<p class="description">安裝Material-UI，這是世界上最受歡迎的React UI框架。</p>

Material-UI以 [npm包](https://www.npmjs.com/package/@material-ui/core)。

## NPM

要安裝並保存在 `package.json` 依賴項中，請運行：

```sh
npm install @ material-ui / core
```

請注意， [反應](https://www.npmjs.com/package/react) > = 16.3.0和 [反應-DOM](https://www.npmjs.com/package/react-dom) > = 16.3.0是對等的依賴關係。

## Roboto字體

Material-UI的設計考慮了 [Roboto](https://fonts.google.com/specimen/Roboto) 字體。 所以一定要遵循 [以下說明](/style/typography/#general)。 例如，通過Google Web Fonts：

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500">
```

## 字體圖標

要使用字體 `圖標` 組件，必須先添加 [材質圖標](https://material.io/tools/icons/) 字體。 這裡有 [ 關於如何操作的說明](/style/icons/#font-icons) 。 例如，通過Google Web Fonts：

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

## SVG圖標

要使用預構建的SVG Material圖標，例如 [組件演示](/demos/app-bar/) 中的圖標，您必須先安裝 [@ material-ui / icons](https://www.npmjs.com/package@material-ui/icons) 軟件包：

```sh
npm install @ material-ui / icons
```

## CDN

您可以開始使用具有最少前端基礎架構的Material-UI， 這對於原型設計非常有用。 我們不鼓勵在生產中使用這種方法 - 客戶端必須下載整個庫，無論實際使用哪些組件， 影響性能和帶寬利用率。

#### UMD發布

我們提供兩個通用模塊定義（UMD）文件：

- 一個用於開發：https：//unpkg.com/@material-ui/core/umd/material-ui.development.js
- 一個用於生產：https：//unpkg.com/@material-ui/core/umd/material-ui.production.min.js

您可以按照 [此CDN示例](https://github.com/mui-org/material-ui/tree/master/examples/cdn) 快速開始。