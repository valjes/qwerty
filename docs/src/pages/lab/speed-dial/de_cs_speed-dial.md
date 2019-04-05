---
title: Speed Dial React組件
components: SpeedDial，SpeedDialAction，SpeedDialIcon
---
# 快速撥號

<p class="description">按下時，浮動動作按鈕可以以快速撥號的形式顯示三到六個相關動作。</p>

如果需要超過六個操作，則應使用除FAB之外的其他操作來呈現它們。

## 簡單的快速撥號

浮動操作按鈕可以顯示相關操作。

{{“demo”：“pages / lab / speed-dial / SpeedDials.js”}}

## 自定義關閉圖標

您可以使用 `SpeedDialIcon` 組件的 `圖標` 和 `openIcon` 道具 為關閉和打開狀態提供備用圖標。

{{“demo”：“pages / lab / speed-dial / OpenIconSpeedDial.js”}}

## 持久性動作工具提示

SpeedDialActions工具提示可以持久顯示，這樣用戶無需長按即可在觸摸設備上查看工具提示。

它在所有設備上都可以用於演示目的，但在生產中它可以使用 `isTouch` 邏輯來有條件地設置屬性。

{{“demo”：“pages / lab / speed-dial / SpeedDialTooltipOpen.js”}}