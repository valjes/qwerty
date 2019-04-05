---
title: Popover React組件
components: 成長，流行
---
# 酥料餅

<p class="description">可以使用Popover在另一個上面顯示一些內容。</p>

使用 `Popover` 組件時需要了解的事項： - 組件構建在 [`Modal`](/utils/modal/) 組件之上。 - 與 [`Popper`](/utils/popper/) 組件不同，滾動和單擊距離被阻止。

## 簡單的彈出窗口

{{“demo”：“pages / utils / popover / SimplePopover.js”}}

## 錨操場

使用單選按鈕調整 `anchorOrigin` 和 `transformOrigin` 位置。 您還可以將 `anchorReference` 設置為 `anchorPosition` 或 `anchorEl`。 當它為 `anchorPosition`，組件將代替 `anchorEl`，參考 `anchorPosition` prop，您可以調整它以設置彈出窗口的位置。

{{“demo”：“pages / utils / popover / AnchorPlayground.js”}}

## 鼠標懸停在互動上

我們演示瞭如何使用 `Popover` 組件來實現基於鼠標懸停事件的彈出行為。

{{“demo”：“pages / utils / popover / MouseOverPopover.js”}}

## 渲染道具

這是一個 [渲染道具](https://reactjs.org/docs/render-props.html) 演示，可以跟踪單個彈出窗口的本地狀態。

{{“demo”：“pages / utils / popover / RenderPropsPopover.js”}}