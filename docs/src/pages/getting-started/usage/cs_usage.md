# 用法

<p class="description">立即開始使用React和Material-UI。</p>

Material-UI組件獨立工作。 **它們是自支撐的**，它將注入並僅注入它們需要顯示的樣式。 它們不依賴於任何全局樣式表，例如 [normalize.css](https://github.com/necolas/normalize.css/)，

您可以使用文檔中演示的任何組件。 請參閱每個組件的 [演示頁](/demos/buttons/) ，了解它們應如何導入。

## 快速開始

這是一個讓你入門的簡單例子， **它只是你需要的**：

```jsx
從'react'中導入React;
從'react-dom'導入ReactDOM;
來自'@ material-ui / core / Button'的導入按鈕;

功能App（）{
  return（
    <Button variant="contained" color="primary">
      Hello World
    </Button>
  ）;
}

ReactDOM.render（<App />，document.querySelector（'＃app'））;
```

是的，這就是您開始使用所需的一切，正如您在此實時和交互式演示中所看到的：

{{“demo”：“pages / getting-started / usage / Usage.js”，“hideHeader”：true}}

## 全局

使用一些您需要注意的重要全局變量可以改善Material-UI使用體驗。

### 響應元標記

Material-UI首先是移動開發的，我們首先為移動設備編寫代碼，然後根據需要使用CSS媒體查詢擴展組件。 要確保所有設備的正確渲染和触摸縮放，請將響應式視口元標記添加到 `<head>` 元素。

```html
<meta
  name="viewport"
  content="minimum-scale=1, initial-scale=1, width=device-width, shrink-to-fit=no"
/>
```

### CssBaseline

Material-UI提供可選的 [CssBaseline](/style/css-baseline/) 組件。 它修復了瀏覽器和設備之間的一些不一致性，同時為常見的HTML元素提供了更多的自我意義的重置。

## 版本化文檔

本文檔始終反映最新的穩定版Material-UI。 您可以在 [單獨的頁面上找到舊版本的文檔](/versions/)。

## 下一步

現在您已經了解了基本設置，現在是時候了解更多信息：

- 如何提供 [Material Design字體和排版](/style/typography/)。
- 如何利用 [主題解決方案](/customization/themes/)。
- 如何 [覆蓋](/customization/overrides/) 組件的外觀。