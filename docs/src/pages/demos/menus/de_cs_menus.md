---
title: 菜單反應組件
components: Menu，MenuItem，MenuList，ClickAwayListener，Popover，Popper
---
# 菜單

<p class="description">菜單顯示臨時曲面上的選項列表。</p>

A [菜單](https://material.io/design/components/menus.html) 顯示臨時表面上的選項列表。 當用戶與按鈕，操作或其他控件交互時，它們會出現。

## 簡單的菜單

默認情況下，簡單菜單在錨元素上打開（此選項可以通過props更改）。 當靠近屏幕邊緣時，簡單的菜單垂直重新對齊，使所有菜單項都完全可見。

選擇一個選項應該立即提交選項並關閉菜單。

**消歧**：與簡單菜單相比，簡單對話框可以顯示與列表項可用選項相關的其他詳細信息，或提供與主任務相關的導航或正交操作。 雖然它們可以顯示相同的內容，但簡單的菜單比簡單的對話框更受歡迎，因為簡單的菜單對用戶的當前上下文的破壞性較小。

{{“demo”：“pages / demos / menus / SimpleMenu.js”}}

## 精選菜單

如果用於項目選擇，則打開時，簡單菜單會嘗試將當前所選菜單項與錨元素垂直對齊。 使用 `選擇的` 屬性（來自 [ListItem](/api/list-item/)）設置當前選擇的菜單項。

{{“demo”：“pages / demos / menus / SimpleListMenu.js”}}

如果簡單菜單中的文本換行到第二行，請使用簡單的對話框。 簡單對話框可以包含不同高度的行。

## 最大高度菜單

如果菜單的高度阻止顯示所有菜單項，則菜單可以在內部滾動。

{{“demo”：“pages / demos / menus / LongMenu.js”}}

## MenuList組成

`Menu` 組件在內部使用 `Popover` 組件。 但是，您可能希望使用不同的定位策略，或者不阻止滾動。 為了滿足這些需求，我們公開了一個可以組成的 `MenuList` 組件，在本例中有 `Popper`。

`MenuList` 組件的主要職責是處理焦點。

{{“demo”：“pages / demos / menus / MenuListComposition.js”}}

## 自定義MenuItem

`MenuItem` 是一個包含 `ListItem` 的包裝器，帶有一些額外的樣式。 您可以使用與 `MenuItem` 組件相同的列表組合功能：

{{“demo”：“pages / demos / menus / ListItemComposition.js”}}

## 改變轉型

完全使用不同的過渡。

{{“demo”：“pages / demos / menus / FadeMenu.js”}}

## 渲染道具

這是一個 [渲染道具](https://reactjs.org/docs/render-props.html) 演示， 跟踪單個菜單的本地狀態。

{{“demo”：“pages / demos / menus / RenderPropsMenu.js”}}