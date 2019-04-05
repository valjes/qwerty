---
title: 抽屜反應組件
components: 抽屜，SwipeableDrawer
---
# 抽屜

<p class="description">導航抽屜可以訪問您應用中的目的地。側板是包含附加內容的表面，其固定在屏幕的左邊緣或右邊緣。</p>

[導航抽屜](https://material.io/design/components/navigation-drawer.html) 提供對目的地和應用功能的訪問，例如切換帳戶。 它們可以永久在屏幕上，也可以通過導航菜單圖標進行控制。

[側板](https://material.io/design/components/sheets-side.html) 是主要用於平板電腦和台式機的輔助表面。

## 臨時抽屜

臨時導航抽屜可以打開或關閉。 默認情況下關閉，抽屜暫時打開所有其他內容，直到選擇一個部分。

單擊疊加或按Esc鍵可取消抽屜。 它在選擇一個項目時關閉，通過控制 `打開` 道具來處理。

{{“demo”：“pages / demos / drawers / TemporaryDrawer.js”}}

## 可滑動的臨時抽屜

您可以使用 `SwipeableDrawer` 組件使抽屜可以滑動。

該組件帶有2 kB gzip負載開銷。 一些低端移動設備無法以60 FPS的速度跟隨手指。 您可以使用 `disableBackdropTransition` 屬性來提供幫助。

{{“demo”：“pages / demos / drawers / SwipeableTemporaryDrawer.js”}}

我們在此文檔網站上使用以下屬性集來獲得組件的最佳可用性： - iOS託管在高端設備上。 我們可以在不丟幀的情況下啟用背景轉換。 表現將足夠好。 - iOS具有“輕掃回去”功能，與發現功能相混淆。 我們必須禁用它。

```jsx
const iOS = process.browser && /iPad|iPhone|iPod/.test(navigator.userAgent）;

<SwipeableDrawer disableBackdropTransition={!iOS} disableDiscovery={iOS} />
```

## 響應抽屜

`隱藏` 響應輔助組件允許根據屏幕寬度顯示不同類型的抽屜。 顯示 `臨時` 抽屜用於小屏幕，而 `永久` 抽屜顯示用於較寬屏幕。

{{“demo”：“pages / demos / drawers / ResponsiveDrawer.js”，“iframe”：true}}

## 永久抽屜

永久導航抽屜始終可見並固定在左邊緣，與內容或背景位於同一高度。 他們無法關閉。

永久導航抽屜是 **桌面默認推薦**。

### 全高導航

應用程序專注於使用從左到右層次結構的信息消費。

{{“demo”：“pages / demos / drawers / PermanentDrawerLeft.js”，“iframe”：true}}

{{“demo”：“pages / demos / drawers / PermanentDrawerRight.js”，“iframe”：true}}

### 剪輯在應用欄下

應用專注於生產力，需要在整個屏幕上保持平衡。

{{“demo”：“pages / demos / drawers / ClippedDrawer.js”，“iframe”：true}}

## 持久的抽屜

持久導航抽屜可以打開或關閉。 抽屜與內容位於同一表面高度上。 它默認關閉，通過選擇菜單圖標打開，並保持打開狀態直到用戶關閉。 從操作到操作和會話到會話記住抽屜的狀態。

當抽屜位於頁面網格之外並打開時，抽屜會強制其他內容更改大小並適應較小的視口。

對於比移動設備更大的尺寸，可以使用持久性導航抽屜。 對於具有多級層次結構且需要使用向上箭頭進行導航的應用，建議不要使用它們。

{{“demo”：“pages / demos / drawers / PersistentDrawerLeft.js”，“iframe”：true}}

{{“demo”：“pages / demos / drawers / PersistentDrawerRight.js”，“iframe”：true}}

## 迷你變體抽屜

在此變體中，持久性導航抽屜會更改其寬度。 它的靜止狀態是一個迷你抽屜，與內容相同，由應用欄夾住。 展開後，它將顯示為標準持久性導航抽屜。

對於需要快速選擇訪問內容的應用部分，建議使用mini變體。

{{“demo”：“pages / demos / drawers / MiniDrawer.js”，“iframe”：true}}