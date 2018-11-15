---
title: Button React組件
components: Button，IconButton，ButtonBase，Zoom
---
# 鈕扣

<p class="description">按鈕允許用戶只需輕按一下即可採取行動並做出選擇。</p>

[按鈕](https://material.io/design/components/buttons.html) 傳達用戶可以採取的操作。 它們通常放置在您的UI中，例如： - 對話框 - 模態窗口 - 表單 - 卡片 - 工具欄

## 文字按鈕

[文本按鈕](https://material.io/design/components/buttons.html#text-button) 通常用於不太明顯的操作，包括那些位於：

- 在對話框中
- 在卡片中

在卡片中，文本按鈕有助於保持對卡片內容的重視。

{{“demo”：“pages / demos / buttons / TextButtons.js”}}

## 概述按鈕

[概述按鈕](https://material.io/design/components/buttons.html#outlined-button) 是中等強調按鈕。 它們含有很重要，行動 而不是一個應用程序的主要作用。

### 備擇方案

概述按鈕也是包含按鈕的低重點替代品， 或更高強度替代文本按鈕。

{{“demo”：“pages / demos / buttons / OutlinedButtons.js”}}

## 包含按鈕

[包含的按鈕](https://material.io/design/components/buttons.html#contained-button) 具有高強度，通過使用高程和填充來區分。 它們包含應用程序的主要操作。

此演示的最後一個示例顯示瞭如何使用上傳按鈕。

{{“demo”：“pages / demos / buttons / ContainedButtons.js”}}

## 浮動動作按鈕

[浮動動作按鈕](https://material.io/design/components/buttons-floating-action-button.html) （FAB）在屏幕上執行主要或最常見的動作。 它出現在所有屏幕內容的前面，通常是一個圓形，中間有一個圖標。 FAB有三種類型：常規，迷你和擴展。

如果它是最適合呈現屏幕主要操作的方式，則僅使用FAB。

每個屏幕僅建議一個浮動操作按鈕來表示最常見的操作。

{{“demo”：“pages / demos / buttons / FloatingActionButtons.js”}}

默認情況下，浮動操作按鈕會在屏幕上顯示為擴展材料。

跨越多個橫向屏幕（例如標籤式屏幕）的浮動操作按鈕應該短暫消失，然後如果其動作發生變化則重新出現 。

可以使用縮放轉換來實現此目的。 請注意，由於同時觸發退出和輸入 動畫，我們使用 `enterDelay` 允許傳出的浮動動作按鈕 動畫在新動畫進入之前完成。

{{“demo”：“pages / demos / buttons / FloatingActionButtonZoom.js”}}

## 圖標按鈕

圖標按鈕通常位於應用欄和工具欄中。

圖標也適用於切換按鈕，允許選擇單個選項或取消選擇 ，例如向項目添加或刪除星標。

{{“demo”：“pages / demos / buttons / IconButtons.js”}}

## 尺寸

花式更大或更小的按鈕？ 使用 `尺寸` 或 `迷你` 屬性。

{{“demo”：“pages / demos / buttons / ButtonSizes.js”}}

### 有像和標籤的按鈕

有時您可能希望為某個按鈕添加圖標以增強應用程序的用戶體驗，因為我們比純文本更容易識別徽標。 例如，如果您有刪除按鈕，則可以使用垃圾箱圖標對其進行標記。

{{“demo”：“pages / demos / buttons / IconLabelButtons.js”}}

## 定制按鈕

如果您一直在閱讀 [覆蓋文檔頁面](/customization/overrides/) 但是您沒有自信地跳入， 這裡是如何使用類， 和使用主題來更改Button的主要顏色的示例;以及Bootstrap樣式按鈕。

{{“demo”：“pages / demos / buttons / CustomizedButtons.js”}}

## 複雜的按鈕

文本按鈕，包含按鈕，浮動動作按鈕和圖標按鈕構建在同一組件之上： `ButtonBase`。 您可以利用此較低級別組件來構建自定義交互。

{{“demo”：“pages / demos / buttons / ButtonBases.js”}}

## 第三方路由庫

一個常見的用例是使用按鈕觸發導航到新頁面。 `ButtonBase` 組件提供了處理此用例的屬性： `組件`。 考慮到我們的許多交互式組件的依賴 `ButtonBase`，你應該是 能夠利用它無處不在：

```jsx
進口 { Link } 從“反應路由器-DOM'
導入按鈕從”@材料-UI /核心/按鈕';

<Button component={Link} to="/open-collective">
  鏈接
</Button>
```

或者如果您想避免屬性衝突：

```jsx
進口 { Link } 從“反應路由器-DOM'
導入按鈕從”@材料-UI /核心/按鈕';

const MyLink = props => <Link to="/open-collective" {...props} />

<Button component={MyLink}>
  Link
</Button>
```

*注意：創建 `MyLink` 是必要的，以防止意外卸載。 你可以閱讀更多關於它的 [位置](/guides/composition/#component-property)。*