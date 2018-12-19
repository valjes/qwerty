---
title: 底部導航反應組件
components: BottomNavigation，BottomNavigationAction
---
# 底部導航

<p class="description">底部導航欄允許在應用程序中的主要目的地之間移動。</p>

[底部導航](https://material.io/design/components/bottom-navigation.html) 條顯示屏幕底部的三到五個目的地。 每個目標都由一個圖標和一個可選的文本標籤表示。 點擊底部導航圖標時，用戶將進入與該圖標關聯的頂級導航目標。

## 底部導航

當只有 **3個** 動作時，始終顯示圖標和文本標籤。

{{“demo”：“pages / demos / bottom-navigation / SimpleBottomNavigation.js”}}

## 沒有標籤的底部導航

如果有 **4** 或 **個5個** 操作，則僅將非活動視圖顯示為圖標。

{{“demo”：“pages / demos / bottom-navigation / LabelBottomNavigation.js”}}