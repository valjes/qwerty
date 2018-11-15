---
title: Portal React組件
components: 門戶
---
# 門戶

<p class="description">門戶網站組件將其子項呈現為當前組件層次結構之外的新“子樹”。</p>

門戶組件的子項將附加到指定的 `容器`。

該組件由 [`Modal`](/utils/modal/) 和 [`Popper`](/utils/popper/) 組件在內部使用。 在服務器上，不會呈現內容。 您必須等待客戶端對帳才能看到孩子。

## 簡單的門戶

{{“demo”：“pages / utils / portal / SimplePortal.js”}}