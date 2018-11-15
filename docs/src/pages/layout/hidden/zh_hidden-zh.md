---
title: 隱藏的React組件
components: 隱
---
# 隱

<p class="description">使用我們隱藏的實用程序快速響應地切換組件的可見性值。</p>

所有元素都是可見的，除非 **明確隱藏**。 為了簡化與 [響應斷點](/layout/basics/)集成，此組件可用於隱藏任何內容，或者您​​可以將它與我們的 [`Grid`](/layout/grid/) 組件結合使用。

## 這個怎麼運作

隱蔽工程與一系列斷點例如 `xsUp` 或 `mdDown`，或一個或多個斷點例如 `只='SM'` 或 `只= {['MD'，'XL']}`。 可以同時使用範圍和單個斷點來實現非常自定義的行為。 範圍包括指定的斷點。

```js
innerWidth | xs sm md lg xl
            | -------- | -------- | -------- | -------- | ----- --->
寬度| xs | sm | md | lg | xl

smUp |顯示|隱藏
mdDown |隱藏|節目

```

## 實現

### JS

默認情況下，使用 `js` 實現，響應性地隱藏基於使用監視屏幕大小的 [`withWidth（）`](/layout/breakpoints/#withwidth-) 高階組件的內容。 除非滿足斷點，否則這樣做的好處是根本不呈現任何內容。

### CSS

如果您正在使用服務器端呈現，則可以設置 `implementation =“css”` 如果您不希望瀏覽器在屏幕上重新流動您的內容。

## 斷點了

使用任何斷點 `高達` 屬性，給定 *孩子* 將被隱藏 *或高於* 的斷點。

{{“demo”：“pages / layout / hidden / BreakpointUp.js”}}

## 斷點下來

使用任何斷點 `向下` 屬性，給定 *孩子* 將被隱藏 *或低於* 的斷點。

{{“demo”：“pages / layout / hidden / BreakpointDown.js”}}

## 僅限斷點

利用斷點 `只有` 屬性，給定 *孩子* 將被隱藏 *在* 指定的斷點（多個）。

在 `只有` 屬性可以以兩種方式使用： -列表中的單個斷點-列出斷點的陣列

{{“demo”：“pages / layout / hidden / BreakpointOnly.js”}}

## 與網格集成

在不同的響應斷點處更改 `Grid` 是很常見的，在許多情況下，您希望隱藏其中的一些元素。

{{“demo”：“pages / layout / hidden / GridIntegration.js”}}