---
components: 活版印刷
---
# 活版印刷

<p class="description">使用排版技術盡可能清晰有效地展示您的設計和內容。</p>

一次太多的類型大小和样式會破壞任何佈局。 [印刷比例](https://material.io/design/typography/#type-scale) 具有一組有限的類型尺寸，它們與佈局網格一起很好地協同工作。

## 一般

Material-UI會自動加載 *Roboto* 字體 **而不是**。 開發人員負責加載其應用程序中使用的所有字體。 Roboto Font有一些簡單的入門方法。

## Roboto Font CDN

下面顯示的是用於從CDN加載Roboto字體的示例鏈接標記。

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500">
```

## 用npm安裝

你可以 [安裝](https://www.npmjs.com/package/typeface-roboto) 鍵入在終端下面的命令：

`npm install typeface-roboto --save`

然後，您可以在入口點導入它。

```js
import'typeface-roboto';
```

有關更多信息，請查看 [字體](https://github.com/KyleAMathews/typefaces/tree/master/packages/roboto) 項目。

⚠️使用這種方法時要小心。 確保您的捆綁包不會急於加載所有字體變體（100/300/400/500/700/900，斜體/常規，SVG / woff）。 內聯所有字體文件可以顯著增加捆綁包的大小。 Material-UI默認排版配置僅依賴於300,400和500字體權重。

## 零件

{{“demo”：“pages / style / typography / Types.js”}}

### 棄用的變體

{{“demo”：“pages / style / typography / DeprecatedTypes.js”}}

## 主題

在某些情況下，您可能無法使用 `Typography` 組件。 希望您可以利用主題的 [`排版`](/customization/default-theme/?expend-path=$.typography) 鍵。

{{“demo”：“pages / style / typography / TypographyTheme.js”}}

## 遷移到排版v2

材料設計規範因變體名稱和样式而發生變化。 為了實現平滑過渡，我們保留舊變體和重新設計的變體以實現向後兼容性，但我們記錄了棄用警告。 我們將在下一個主要版本v4.0.0（2019年第一季度）中刪除舊的排版變體。

### 策略

要立即切換到排版v2，您只需傳遞 `useNextVariants：true` 當調用 `createMuiTheme`：

```js
常量主題= createMuiTheme（{
  排版： {
    useNextVariants: true,
  }，
}）;
```

或設置 `窗口。__MUI_USE_NEXT_TYPOGRAPHY_VARIANTS__ =真;` 如果您不使用主題。

根據以下映射，這將使用新變體而不是舊變體：

```sh
display4 => h1
display3 => h2
display2 => h3
display1 => h4
headline => h5
title => h6
subheading => subtitle1
body2 => body1
body1（默認）=> body2（默認）
```

請注意，如果您使用其中一個舊版本，則會記錄棄用警告。 我們建議您使用推薦的變體替換那些舊的變體，為下一個主要版本做好準備。 有關如何使用全局主題的更多信息，請參見 [主題](/customization/themes/)。