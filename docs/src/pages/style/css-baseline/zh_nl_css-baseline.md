---
components: CssBaseline
---
# CSS基線

<p class="description">Material-UI提供了一個CssBaseline組件，用於啟動優雅，一致且簡單的基線。</p>

您可能熟悉 [normalize.css](https://github.com/necolas/normalize.css)，HTML元素和屬性樣式規範化的集合。

```jsx
從'react'中導入React;
從'@ material-ui / core / CssBaseline'導入CssBaseline;

函數MyApp（）{
  return（
    <React.Fragment>
      <CssBaseline />
      {/ *你申請的其餘部分* /}
    </React.Fragment>
  ）;
}

導出默認MyApp;
```

## 途徑

### 頁

更新 `<html>` 和 `<body>` 元素以提供更好的頁面範圍默認值。 更具體地說： - 刪除所有瀏覽器中的邊距。 - 應用默認的“材質設計”背景顏色。 它使用 [`theme.palette.background.default`](/customization/default-theme/?expend-path=$.palette.background) 用於標准設備，白色背景用於打印設備。

### 佈局

- `box-sizing` 全局設置在 `<html>` 元素到 `邊框`。 聲明每個元素（包括 `* ::` 之前和 `* ::` 之後）繼承此屬性，這可確保由於填充或邊框而永遠不會超出聲明的元素寬度。

### 活版印刷

- 啟用字體抗鋸齒功能可以更好地顯示Roboto字體。
- `<html>`上沒有聲明基本字體大小，但假定為16px（瀏覽器默認值）。 您可以在主題文檔</a> 頁面的 了解更改 `<html>` 默認字體大小的含義。</li> </ul>