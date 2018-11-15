---
title: Modal React組件
components: 語氣
---
# 語氣

<p class="description">模態組件為創建對話框，彈出窗口，燈箱或其他任何東西提供了堅實的基礎。</p>

該組件在背景組件前面呈現其 `個子節點` 節點。

`模態` 提供了一些有用的功能，而不僅僅使用 [`Portal`](/utils/portal/) 組件和一些樣式： - 管理對話框堆疊時，一次一個是不夠的。 - 創建背景，用於禁用模式下的交互。 - 妥善管理焦點;移動到模態內容， 並保持它直到模態關閉。 - 它會在打開時禁用頁面內容的滾動。 - 自動添加適當的ARIA角色。

該組件與 [反應疊加](https://react-bootstrap.github.io/react-overlays/#modals)共享許多概念。

## 簡單模態

{{“demo”：“pages / utils / modal / SimpleModal.js”}}