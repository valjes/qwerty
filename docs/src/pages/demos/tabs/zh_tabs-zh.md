---
title: 標籤反應組件
components: 標籤，標籤
---
# 標籤

<p class="description">選項卡可以輕鬆瀏覽和切換不同的視圖。</p>

[選項卡](https://material.io/design/components/tabs.html) 組織並允許在相關且處於相同層次結構的內容組之間進行導航。

## 簡單的標籤

一個沒有多餘裝飾的簡單例子。

{{“demo”：“pages / demos / tabs / SimpleTabs.js”}}

### 包裹標籤

長標籤將自動換行標籤。 如果標籤的標籤太長，它將溢出並且文本將不可見。

{{“demo”：“pages / demos / tabs / TabsWrappedLabel.js”}}

### 禁用標籤

可以通過設置 `禁用` 屬性來禁用選項卡。

{{“demo”：“pages / demos / tabs / DisabledTabs.js”}}

## 固定標籤

固定標籤應與有限數量的標籤一起使用，並且當一致的放置將有助於肌肉記憶。

### 全屏寬度

`fullWidth` 屬性應該用於較小的視圖。 此演示還使用 [react-swipeable-views](https://github.com/oliviertassinari/react-swipeable-views) 來動畫Tab過渡，並允許在觸摸設備上滑動標籤。

{{“demo”：“pages / demos / tabs / FullWidthTabs.js”}}

### 中心

`居中` 屬性應該用於較大的視圖。

{{“demo”：“pages / demos / tabs / CenteredTabs.js”}}

## 可滾動標籤

### 自動滾動按鈕

左右滾動按鈕將自動顯示在桌面上並隱藏在移動設備上。 （基於視口寬度）

{{“demo”：“pages / demos / tabs / ScrollableTabsButtonAuto.js”}}

### 強制滾動按鈕

無論視口寬度如何，都將顯示左右滾動按鈕。

{{“demo”：“pages / demos / tabs / ScrollableTabsButtonForce.js”}}

### 防止滾動按鈕

永遠不會出現左右滾動按鈕。 必須通過用戶代理滾動機制（例如左/右滑動，移位 - 鼠標滾輪等）啟動所有滾動

{{“demo”：“pages / demos / tabs / ScrollableTabsButtonPrevent.js”}}

## 圖標選項卡

標籤標籤可以是所有圖標或全文。

{{“demo”：“pages / demos / tabs / IconTabs.js”}} {{“demo”：“pages / demos / tabs / IconLabelTabs.js”}}

## 導航標籤

默認情況下，選項卡使用 `按鈕` 元素，但您可以提供自己的自定義標記或組件。 以下是實現選項卡式導航的示例：

{{“demo”：“pages / demos / tabs / NavTabs.js”}}

## 自定義標籤

如果您已經閱讀了 [覆蓋文檔第](/customization/overrides/) 頁但是沒有自信地跳入，這裡是一個如何更改選項卡主要顏色的示例。 以下演示與 [Ant Design UI](https://ant.design/components/tabs/)匹配。

{{“demo”：“pages / demos / tabs / CustomizedTabs.js”}}