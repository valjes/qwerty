# 最小化捆綁包大小

<p class="description">了解有關可用於減少捆綁包大小的工具的詳細信息。</p>

## 捆綁尺寸很重要

Material-UI的包大小非常嚴重，因此 [大小限制](https://github.com/ai/size-limit) 用於防止引入任何大小的回歸。 每次提交時都會檢查包的大小：

- 導入 **所有組件**。 這讓我們可以發現任何 [不需要的包大小增加](https://github.com/mui-org/material-ui/blob/master/.size-limit.js#L30)。
- 導入 **單個組件**。 這讓我們估計 [核心依賴關係](https://github.com/mui-org/material-ui/blob/master/.size-limit.js#L24)的開銷。 （造型，主題等：~18 kB gzipped）

## 如何減少捆綁尺寸？

為方便起見，Material-UI在頂級 `material-ui` 導入中公開其完整API。 使用這是好的，如果你有樹搖晃的工作，然而，在樹上搖晃不支持或在構建鏈構成的情況下， **這將導致整個庫及其依賴被列入** 在您的客戶端包。

您有幾種方法可以克服這種情況：

### 選項1

您可以直接從 `material-ui /` 導入，以避免拉入未使用的模塊。 例如，而不是：

```js
從'@ material-ui / core'導入 { Button, TextField };
```

使用：

```js
從'@ material-ui / core / Button'導入按鈕;
從'@ material-ui / core / TextField'導入TextField;
```

雖然以這種方式直接導入不使用 [`material-ui / index.js`](https://github.com/mui-org/material-ui/blob/master/packages/material-ui/src/index.js)的導出，但此文件可以作為公共哪些模塊的方便參考。 任何未在此列出的內容都應被視為 **私有**，如有更改，恕不另行通知。 例如， `Tabs` 組件是公共模塊，而 `TabIndicator` 是私有模塊。

### 選項2

另一個選擇是繼續使用縮短的導入，如下所示，但由於 **Babel插件**，仍然優化了捆綁的大小：

```js
從'@ material-ui / core'導入 { Button, TextField };
```

選擇以下插件之一：

- [babel-plugin-import](https://github.com/ant-design/babel-plugin-import) 可以自定義，並且有足夠的調整與Material-UI一起使用。
- [babel-transform-imports](https://bitbucket.org/amctheatres/babel-transform-imports) 有一個不同的api而不是 `babel-plugin-import` 但是做同樣的事情。
- [babel-plugin-lodash](https://github.com/lodash/babel-plugin-lodash) 旨在開箱即用，包含所有 `package.json`。

**重要說明**：在向項目添加樹搖動功能之前，這兩個選項 *都應該是臨時的*。

## ECMAScript中

在npm上發布的包是 **轉換為**，帶有 [Babel](https://github.com/babel/babel)，以考慮 [支持的平台](/getting-started/supported-platforms/)。

我們還發布了第二個版本的組件，以針對 **常綠瀏覽器**。 您可以在 [`/ es` 文件夾](https://unpkg.com/@material-ui/core/es/)下找到此版本。 所有非官方語法都被轉換為 [ECMA-262標準](https://www.ecma-international.org/publications/standards/Ecma-262.htm)，僅此而已。 這可用於製作針對不同瀏覽器的單獨捆綁包。 較舊的瀏覽器將需要更多的JavaScript功能進行轉換，這會增加捆綁包的大小。 ES2015運行時功能不包含任何填充。 IE11 +和常青瀏覽器支持所有必要的功能。 如果您需要支持其他瀏覽器，請考慮使用 [`@ babel / polyfill`](https://www.npmjs.com/package/@babel/polyfill)。

⚠️為了最小化在用戶的束的重複代碼，我們 **強烈阻止** 從使用庫作者 `/ ES` 的文件夾。