---
title: Tooltip React組件
components: 提示
---
# 提示

<p class="description">當用戶將鼠標懸停在上方，聚焦或點按元素時，工具提示會顯示信息性文本。</p>

激活時， [工具提示](https://material.io/design/components/tooltips.html) 顯示標識元素的文本標籤，例如其功能描述。

## 簡單的工具提示

{{“demo”：“pages / demos / tooltips / SimpleTooltips.js”}}

## 定位工具提示

`工具提示` 有12個 **位置** 選擇。 他們沒有方向箭頭;相反，它們依靠從源頭髮出的運動來傳達方向。

{{“demo”：“pages / demos / tooltips / PositionedTooltips.js”}}

## 受控工具提示

可以使用 `打開`， `的OnOpen` 和 `的OnClose` 屬性來控制工具提示的行為。

{{“demo”：“pages / demos / tooltips / ControlledTooltips.js”}}

## 觸發器

您可以定義導致工具提示顯示的事件類型。

{{“demo”：“pages / demos / tooltips / TriggersTooltips.js”}}

## 轉變

使用不同的過渡。

{{“demo”：“pages / demos / tooltips / TransitionsTooltips.js”}}

## 顯示和隱藏

當用戶的鼠標懸停在元素上時，工具提示通常立即顯示，並在用戶的鼠標離開時立即隱藏。 可以通過屬性 `enterDelay` 和 `leaveDelay`添加顯示或隱藏工具提示的延遲，如上面的受控工具提示演示中所示。

在移動設備上，當用戶長按元素並在延遲1500ms後隱藏時，將顯示工具提示。 您可以使用 `disableTouchListener` 屬性禁用此功能。

{{“demo”：“pages / demos / tooltips / DelayTooltips.js”}}

## 禁用元素

默認情況下，禁用的元素（如 `按鈕` 不會觸髮用戶交互，因此 `工具提示` 不會在正常事件（如懸停）上激活。 要容納已禁用的元素，請添加一個簡單的包裝元素，如 `span`。

{{“demo”：“pages / demos / tooltips / DisabledTooltips.js”}}

## 自定義工具提示

{{“demo”：“pages / demos / tooltips / CustomizedTooltips.js”}}

## 可變寬度

`工具提示` 默認包裝長文本以使其可讀。

{{“demo”：“pages / demos / tooltips / VariableWidth.js”}}