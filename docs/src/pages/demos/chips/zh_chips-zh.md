---
title: Chip React組件
components: 芯片
---
# 芯片

<p class="description">芯片是表示輸入，屬性或動作的緊湊元素。</p>

[芯片](https://material.io/design/components/chips.html) 允許用戶輸入信息，進行選擇，過濾內容或觸發操作。

雖然這裡作為獨立組件包含在內，但最常見的用途是在某種形式的輸入中，因此這裡演示的一些行為不會在上下文中顯示。

## 芯片

使用圖像頭像，SVG圖標頭像，“字母”和（字符串）頭像的芯片示例。

- 具有 `onClick` 屬性的芯片定義了焦點，懸停和單擊時的外觀變化。
- 定義了 `onDelete` 屬性的芯片將顯示一個刪除圖標，該圖標會在懸停時更改外觀。

{{“demo”：“pages / demos / chips / Chips.js”}}

### 概述芯片

概述的芯片提供了另一種風格。

{{“demo”：“pages / demos / chips / OutlinedChips.js”}}

## 籌碼遊樂場

{{“demo”：“pages / demos / chips / ChipsPlayground.js”}}

## 芯片陣列

從值數組渲染多個Chips的示例。 刪除芯片會將其從陣列中刪除。 請注意，由於未定義 `onClick` 屬性，因此可以聚焦Chip，但在單擊或觸摸時不會獲得深度。

{{“demo”：“pages / demos / chips / ChipsArray.js”}}