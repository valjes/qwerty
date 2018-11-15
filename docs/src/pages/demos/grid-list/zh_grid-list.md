---
title: 網格列表反應組件
components: GridList，GridListTile，GridListTileBar，ListSubheader，IconButton
---
# 網格列表

<p class="description">網格列表在有組織的網格中顯示圖像集合。</p>

[網格列表](https://material.io/design/components/image-lists.html) 表示重複模式中的項目集合。 它們有助於提高對所持內容的視覺理解。

## 僅圖像網格列表

可滾動圖像的一個簡單示例 `GridList`。

{{“demo”：“pages / demos / grid-list / ImageGridList.js”，“hideEditButton”：true}}

## 帶有標題欄的網格列表

此示例演示如何使用 `GridListTileBar` 為每個 `GridListTile`添加疊加層。 疊加層可以容納 `標題` `字幕` 和輔助動作 - 在這個例子中是 `IconButton`。

{{“demo”：“pages / demos / grid-list / TitlebarGridList.js”，“hideEditButton”：true}}

## 高級網格列表

此示例演示了“特色”圖塊，使用 `行` 和 `列` 道具調整圖塊的大小，並使用 `填充` 道具調整間距。 圖塊具有自定義標題欄，位於頂部，並帶有自定義漸變 `titleBackground`。 輔助操作 `IconButton` 位於左側。

{{“demo”：“pages / demos / grid-list / AdvancedGridList.js”，“hideEditButton”：true}}

## 單行網格列表

此示例演示了水平可滾動的單行網格圖像列表。 不鼓勵水平滾動網格列表，因為滾動會干擾典型的閱讀模式，從而影響理解。 一個值得注意的例外是水平滾動的單行網格圖像列表，例如圖庫。

{{“demo”：“pages / demos / grid-list / SingleLineGridList.js”，“hideEditButton”：true}}