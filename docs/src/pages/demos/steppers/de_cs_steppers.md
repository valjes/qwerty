---
title: Stepper React組件
components: MobileStepper，Step，StepButton，StepConnector，StepContent，StepIcon，StepLabel，Stepper
---
# 踏步

<p class="description">步進器通過編號步驟傳達進度。</p>

[步進器](https://material.io/archive/guidelines/components/steppers.html) 顯示一系列邏輯和編號步驟的進度。 它們也可用於導航。 保存步驟後，步進器可能會顯示瞬態反饋消息。

**步驟的類型**

- 可編輯
- 不可編輯
- 移動
- 可選的

**步進式的類型**

- 橫
- 垂直
- 線性
- 非線性

## 水平線性

可以通過將當前步驟索引（從零開始）作為 `activeStep` 屬性來控制 `步進器`。 `使用 <code>方向` 屬性設置步進器</code> 方向。

此示例還通過在第二個 `Step` 組件上放置 `可選` 屬性來顯示可選步驟的使用。 請注意，您可以在跳過可選步驟時進行管理。 一旦為特定步驟確定了這一點，就必須設置 `completed ={false}` 表示即使活動步驟索引超出了可選步驟，它也不會實際完成。

{{“demo”：“pages / demos / steppers / Horizo​​ntalLinearStepper.js”}}

## 水平非線性

非線性步進器允許用戶在任何點輸入多步流程。

此示例類似於常規水平步進器，但步驟不再基於 `activeStep` 屬性自動設置為 `disabled ={true}`。

我們已經使用了 `StepButton` 這裡展示點擊步驟標籤，以及設置 `完成` 標誌然而，由於步驟可以在一個非線性的方式就看你自己的實現要訪問 確定何時完成所有步驟（或者即使他們需要完成）。

{{“demo”：“pages / demos / steppers / Horizo​​ntalNonLinearStepper.js”}}

## 水平線性 - 替代標籤

通過在 `Stepper` 組件上設置 `alternativeLabel` 屬性，可以將標籤放置在步驟圖標下方。

{{“demo”：“pages / demos / steppers / Horizo​​ntalLinearAlternativeLabelStepper.js”}}

## 水平非線性 - 替代標籤

{{“demo”：“pages / demos / steppers / Horizo​​ntalNonLinearAlternativeLabelStepper.js”}}

## 水平非線性 - 錯誤步驟

{{“demo”：“pages / demos / steppers / Horizo​​ntalNonLinearStepperWithError.js”}}

## 垂直步進器

{{“demo”：“pages / demos / steppers / VerticalLinearStepper.js”}}

## 定制步進器

此組件使用自定義的 `StepConnector` 元素，該元素根據 `活動的` 和 `完成的` 狀態更改邊框顏色。

{{“demo”：“pages / demos / steppers / CustomizedStepper.js”}}

## 移動步進

該組件實現了適用於移動設備的緊湊型步進器。 請參閱 [移動步驟](https://material.io/archive/guidelines/components/steppers.html#steppers-types-of-steps) 了解其靈感。

### 移動步進 - 文本

這基本上是正確定位的後退/下一個按鈕。 您必須自己實現文本描述，但是，下面提供了一個示例供參考。

{{“demo”：“pages / demos / steppers / TextMobileStepper.js”}}

### 移動步進器 - 帶旋轉木馬效果的文本

此演示與之前的演示非常相似，不同之處在於使用 [react-swipeable-views](https://github.com/oliviertassinari/react-swipeable-views) 來進行步驟的轉換。

{{“demo”：“pages / demos / steppers / SwipeableTextMobileStepper.js”}}

### 移動步進 - 點

當步數不大時使用點。

{{“demo”：“pages / demos / steppers / DotsMobileStepper.js”}}

### 移動步進 - 進步

當有許多步驟時，或者如果在此過程中需要插入步驟（基於對早期步驟的響應），請使用進度條。

{{“demo”：“pages / demos / steppers / ProgressMobileStepper.js”}}