---
title: Checkbox，Radio，Switch React組件
components: FormControl，FormGroup，FormLabel，FormControlLabel，RadioGroup，Checkbox，Radio，Switch
---
# 選擇控制

<p class="description">選擇控件允許用戶選擇選項。</p>

[選擇控件](https://material.io/design/components/selection-controls.html) 允許用戶完成涉及選擇的任務，例如選擇選項或打開或關閉設置。 選擇控件位於要求用戶做出決定或聲明諸如設置或對話框等首選項的屏幕上。

本節介紹了三種類型的選擇控件：

- **[複選框](#checkboxes)** 允許從一組中選擇多個選項。
- **[單選按鈕](#radio-buttons)** 允許從一個選項中選擇一個選項。
- **[開關](#switches)** 允許打開或關閉選擇。

## 複選框

[複選框](https://material.io/design/components/selection-controls.html#checkboxes) 允許用戶從一組中選擇一個或多個項目。 複選框可用於打開或關閉選項。

如果您有出現在列表中多個選項， 您可以通過使用複選框，而不是打開/關閉開關保留空間。 如果您只有一個選項，請避免使用複選框並使用開/關開關。

{{“demo”：“pages / demos / selection-controls / Checkboxes.js”}}

`複選框` 也可以與標籤描述一起使用，這要歸功於 `FormControlLabel` 組件。

{{“demo”：“pages / demos / selection-controls / CheckboxLabels.js”}}

## 使用FormGroup的複選框

`FormGroup` 是一個有用的包裝器，用於對選擇控件組件進行分組，從而提供更簡單的API。

{{“demo”：“pages / demos / selection-controls / CheckboxesGroup.js”}}

## 單選按鈕

[單選按鈕](https://material.io/design/components/selection-controls.html#radio-buttons) 允許用戶從一組中選擇一個選項。 當用戶需要查看所有可用選項時，使用單選按鈕。 如果可以折疊可用選項，請考慮使用下拉菜單，因為它佔用的空間更少。

單選按鈕應該具有默認選擇的最常用選項。

`RadioGroup` 是一個有用的包裝器，用於對 `Radio` 組件進行分組，這些組件提供了更簡單的API，以及對組的正確鍵盤可訪問性。

{{“demo”：“pages / demos / selection-controls / RadioButtonsGroup.js”}}

### 獨立收音機按鈕

`Radio` 也可以獨立使用，不需要包裝。

{{“demo”：“pages / demos / selection-controls / RadioButtons.js”}}

## 開關

[開關](https://material.io/design/components/selection-controls.html#switches) 打開或關閉單個設置的狀態。 它們是調整移動設置的首選方式。

應該從相應的內聯標籤中清除開關控制的選項以及它所處的狀態 。

{{“demo”：“pages / demos / selection-controls / Switches.js”}}

### 使用FormControlLabel切換

`由於 <code>FormControlLabel` 組件，開關</code> 也可以與標籤描述一起使用。

{{“demo”：“pages / demos / selection-controls / SwitchLabels.js”}}

### 使用FormGroup切換

`FormGroup` 是一個有用的包裝器，用於對選擇控件組件進行分組，從而提供更簡單的API。 但是，我們建議您使用 [複選框](#checkboxes)。

{{“demo”：“pages / demos / selection-controls / SwitchesGroup.js”}}

### 定制開關

如果你一直在閱讀 [覆蓋文檔頁面](/customization/overrides/) 但是你沒有自信地跳進去，這裡有一個如何改變Switch和iOS風格Switch的顏色的例子。

{{“demo”：“pages / demos / selection-controls / CustomizedSwitches.js”}}