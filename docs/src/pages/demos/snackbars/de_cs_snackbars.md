---
title: Snackbar React組件
components: Snackbar，SnackbarContent
---
# 小吃店

<p class="description">Snackbars通過消息提供有關應用程序進程的簡短消息 - 通常位於屏幕底部</p>

[Snackbars](https://material.io/design/components/snackbars.html) 告知用戶應用程序已執行或將要執行的進程。 它們暫時出現在屏幕底部。 它們不應該中斷用戶體驗，也不要求用戶輸入消失。

Snackbars包含與執行操作直接相關的單行文本。 它們可能包含文本操作，但沒有圖標。 您可以使用它們來顯示通知。

#### 頻率

一次只能顯示一個小吃吧。

## 簡單

一個基本的快餐欄，旨在重現Google Keep的零食欄行為。

{{“demo”：“pages / demos / snackbars / SimpleSnackbar.js”}}

## 消息長度

一些小吃店有不同的消息長度。

{{“demo”：“pages / demos / snackbars / LongTextSnackbar.js”}}

## 定位

在某些情況下，小吃店的放置需要更加靈活。

{{“demo”：“pages / demos / snackbars / PositionedSnackbar.js”}}

## 轉變

### 控制方向

改變過渡的方向。 幻燈片是默認過渡。

{{“demo”：“pages / demos / snackbars / DirectionSnackbar.js”}}

### 改變轉型

一起使用不同的過渡。

{{“demo”：“pages / demos / snackbars / FadeSnackbar.js”}}

### 不要阻止浮動操作按鈕

垂直移動浮動操作按鈕以適應零食欄高度。

{{“demo”：“pages / demos / snackbars / FabIntegrationSnackbar.js”}}

### 連續的Snackbars

每 [谷歌的準則](https://material.io/design/components/snackbars.html#snackbars-toasts-usage)：當在第一個顯示被觸發第二小吃吧，首先應該向下的第二個向上的動畫開始前的收縮運動。

{{“demo”：“pages / demos / snackbars / ConsecutiveSnackbars.js”}}

## 定制的Snackbars

如果您一直在閱讀 [覆蓋文檔頁面](/customization/overrides/) 但是您沒有自信地跳入， 這裡是您如何更改Snackbar外觀的示例。

{{“demo”：“pages / demos / snackbars / CustomizedSnackbars.js”}}

## 高級用例

對於更高級的用例，您可能可以利用： - [notistack](https://github.com/iamhosseindhv/notistack) 高度可定制的通知零食欄，可以堆疊在彼此之上