---
title: 網格反應組件
components: 格
---
# 格

<p class="description">Material Design響應式佈局網格適應屏幕尺寸和方向，確保佈局的一致性。</p>

[網格](https://material.io/design/layout/responsive-layout-grid.html) 在佈局之間創建視覺一致性，同時允許各種設計的靈活性。 Material Design的響應式UI基於12列網格佈局。

## 這個怎麼運作

網格系統使用 `Grid` 組件實現： - 它使用 [CSS的Flexible Box模塊](https://www.w3.org/TR/css-flexbox-1/) ，具有很高的靈活性。 - 有兩種類型的佈局： *容器* 和 *項目*。 - 項目寬度以百分比形式設置，因此它們總是相對於其父元素具有流動性和大小。 - 項目具有填充以創建單個項目之間的間距。 - 有五個網格斷點：xs，sm，md，lg和xl。

## 間距

響應網格側重於一致的間距寬度，而不是列寬。 材料設計餘量和列遵循 **8dp** 平方基線網格。 間距可以是8,16,24,32或40dp寬。

{{“demo”：“pages / layout / grid / SpacingGrid.js”}}

## 流體網格

流體網格使用可縮放和調整內容大小的列。 流體網格的佈局可以使用斷點來確定佈局是否需要顯著改變。

### 基本網格

列寬適用於所有斷點（即 `xs` 及以上）。

{{“demo”：“pages / layout / grid / CenteredGrid.js”}}

### 帶斷點的網格

某些列定義了多個寬度，導致佈局在定義的斷點處更改。

{{“demo”：“pages / layout / grid / FullWidthGrid.js”}}

## 互動

下面是一個交互式演示，可讓您探索不同設置的可視結果：

{{“demo”：“pages / layout / grid / InteractiveGrid.js”}}

## 自動佈局

自動佈局使 *項* 公平地共享可用空間。 這也意味著你可以設置一個 *項* 的寬度，其他的將自動調整它的大小。

{{“demo”：“pages / layout / grid / AutoGrid.js”}}

## CSS網格佈局

**CSS網格佈局** 擅長將頁面劃分為主要區域，或者在從HTML基元構建的控件的各個部分之間定義大小，位置和圖層之間的關係。 遺憾的是，CSS網格僅受最新瀏覽器的支持。

{{“demo”：“pages / layout / grid / CSSGrid.js”}}

## 嵌套網格

`容器` 和 `項` 屬性是兩個獨立的布爾值。 它們可以結合起來。

> flex **容器** 是由具有 `flex` 或 `inline-flex`的計算顯示的元素生成的框。 Flex容器的流入子容器稱為flex **items** 並使用flex佈局模型進行佈局。

https://www.w3.org/TR/css-flexbox-1/#box-model

{{“demo”：“pages / layout / grid / NestedGrid.js”}}

## 複雜網格

以下演示不遵循Material Design規範，但說明瞭如何使用網格構建複雜的佈局。

{{“demo”：“pages / layout / grid / ComplexGrid.js”}}

## 限制

### 負利潤率

我們使用負邊距來實現項目之間的間距有一個限制。 如果負餘量超過 `<body>`則會出現水平滾動。 有3種可用的解決方法：1。 不使用間距功能並在用戶空間中實現 `間距={0}` （默認值）。 2。 在父級上添加填充，至少包含間距值：

```jsx
  <body>
    <div style={{ padding: 20 }}>
      <Grid container spacing={40}>
        // ...
      </Grid>
    </div>
  </body>
```

1. 添加 `overflow-x：hidden;` 對父母。

### 白色空間：nowrap;

彈性項目的初始設置為 `min-width：auto`。 當孩子們使用 `白色空間時，它會導致定位衝突：nowrap;`。 您可以遇到以下問題：

```jsx
<Grid item xs>
  <Typography noWrap>
```

為了使項目保持在容器內，您需要設置 `min-width：0`。 實際上，您可以設置 `zeroMinWidth` 屬性：

```jsx
<Grid item xs zeroMinWidth>
  <Typography noWrap>
```

{{“demo”：“pages / layout / grid / AutoGridNoWrap.js”}}