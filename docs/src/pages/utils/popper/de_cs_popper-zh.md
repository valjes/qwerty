---
title: Popper React組件
components: 波普爾
---
# 波普爾

<p class="description">Popper可用於在另一個上面顯示一些內容。 它是react-popper的替代品。</p>

使用 `Popper` 組件時需要了解的事項：

- Poppers依靠第三方庫 [Popper.js](https://github.com/FezVrasta/popper.js) 進行定位。
- 孩子們是文件正文的 [`Portal`](/utils/portal/) ，以避免出現問題。 您可以使用 `disablePortal`禁用此行為。
- 滾動和單擊距離不會像 [`Popover`](/utils/popover/) 組件一樣被阻止。 popper的位置隨視口中的可用區域更新。
- 將 `anchorEl` 作為引用對像傳遞以創建新的 `Popper.js` 實例。

## 簡單波普爾

{{“demo”：“pages / utils / popper / SimplePopper.js”}}

## 滾動遊樂場

{{“demo”：“pages / utils / popper / ScrollPlayground.js”}}

## 定位波普爾

{{“demo”：“pages / utils / popper / PositionedPopper.js”}}

## 沒有過渡波普爾

{{“demo”：“pages / utils / popper / NoTransitionPopper.js”}}

## 偽造的參考物體

`anchorEl` 屬性可以是對偽DOM元素的引用。 您只需要創建一個形狀類似於 [`ReferenceObject`](https://github.com/FezVrasta/popper.js/blob/0642ce0ddeffe3c7c033a412d4d60ce7ec8193c3/packages/popper/index.d.ts#L118-L123)。

突出顯示部分文本以查看popper：

{{“demo”：“pages / utils / popper / FakedReferencePopper.js”}}

## 渲染道具

它是一個 [渲染道具](https://reactjs.org/docs/render-props.html) 演示，可以跟踪單個popper的本地狀態。

{{“demo”：“pages / utils / popper / RenderPropsPopper.js”}}