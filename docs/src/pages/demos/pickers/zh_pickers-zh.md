---
title: 日期選擇器，時間選擇器反應組件
components: 文本域
---
# 拾荒者

<p class="description">拾取器提供了一種從預定集合中選擇單個值的簡單方法。</p>

- 在移動設備上，揀貨員最適合在確認對話框中顯示。
- 對於內聯顯示，例如在表單上，請考慮使用緊湊控件，例如分段下拉按鈕。

#### 注意

我們目前正在回歸 **原生輸入控件**。 如果您有興趣實施或實施了豐富的Material Design Picker和一個非常棒的UX，請告訴我們 [＃4787](https://github.com/mui-org/material-ui/issues/4787) 和 [＃4796](https://github.com/mui-org/material-ui/issues/4796)！ 我們可以在文檔中添加項目的鏈接或演示。 下面是一些部件被 **有為**： - [材料-UI-拾取器](https://github.com/dmtrKovalenko/material-ui-pickers)：日期選取器和時間選擇器。 - [物質 - 時間選擇器](https://github.com/TeamWertarbyte/material-ui-time-picker)：時間選擇器。 - [材料-ui-next-Pickers](https://github.com/chingyawhao/material-ui-next-pickers)：日期選擇器和時間選擇器。

⚠️瀏覽器支持的原生輸入控件 [並不完美](https://caniuse.com/#feat=input-datetime)。

## 選擇日期

`type =“date”`的原生日期選擇器示例，它也可以用作日曆：

{{“demo”：“pages / demos / pickers / DatePickers.js”}}

## 時間選擇器

`type =“time”`本機時間選擇器示例：

{{“demo”：“pages / demos / pickers / TimePickers.js”}}

## 日期 & 時間選擇器

原生日期 & 時間選擇器示例，其中 `type =“datetime-local”`：

{{“demo”：“pages / demos / pickers / DateAndTimePickers.js”}}