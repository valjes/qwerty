---
title: 卡片反應組件
components: 卡，CardActionArea，CardActions，CardContent，CardHeader，CardMedia，Collapse，Paper
---
# 牌

<p class="description">卡片包含有關單個主題的內容和操作。</p>

[卡](https://material.io/design/components/cards.html) 是顯示單個主題的內容和操作的表面。

他們應該易於掃描相關和可操作的信息。 文本和圖像等元素應以明確指示層次結構的方式放置在它們上面。

## 簡單卡

雖然卡可以支持多個操作，UI控件和溢出菜單，但請使用約束並記住卡是更複雜和詳細信息的入口點。

{{“demo”：“pages / demos / cards / SimpleCard.js”}}

## 媒體

使用圖像來加強內容的卡的示例。

{{“demo”：“pages / demos / cards / MediaCard.js”}}

默認情況下，我們使用 `<div>` 元素和 *背景圖像* 來顯示媒體。 在某些情況下可能會出現問題。 例如，您可能希望顯示視頻或響應圖像。 對這些用例使用 `組件` 屬性：

{{“demo”：“pages / demos / cards / ImgMediaCard.js”}}

## UI控件

使用圖標，文本和UI控件明確地調出卡內的補充操作，通常放置在卡的底部。

這是媒體控制卡的一個例子。

{{“demo”：“pages / demos / cards / MediaControlCard.js”}}

## 複雜的互動

在桌面上，卡內容可以擴展。

{{“demo”：“pages / demos / cards / RecipeReviewCard.js”}}