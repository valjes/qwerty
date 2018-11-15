---
title: 文本字段反應組件
components: FilledInput，FormControl，FormHelperText，Input，InputAdornment，InputBase，InputLabel，OutlinedInput，TextField
---
# 文字字段

<p class="description">文本字段允許用戶輸入和編輯文本。</p>

[文本字段](https://material.io/design/components/text-fields.html) 允許用戶在UI中輸入文本。 它們通常出現在表單和對話框中。

## 文本域

`TextField` 包裝器組件是一個完整的表單控件，包括標籤，輸入和幫助文本。

{{“demo”：“pages / demos / text-fields / TextFields.js”}}

## 概述

`TextField` 支持輪廓樣式。

{{“demo”：“pages / demos / text-fields / OutlinedTextFields.js”}}

## 填充

`TextField` 支持填充樣式。

{{“demo”：“pages / demos / text-fields / FilledTextFields.js”}}

## 組件

`的TextField` 是由更小的部件（的 [`FormControl`](/api/form-control/)， [`輸入`](/api/input/)， [`FilledInput`](/api/filled-input/)， [`InputLabel`](/api/input-label/)， [`OutlinedInput`](/api/outlined-input/)， 和 [`FormHelperText`](/api/form-helper-text/) ）您可以直接利用來顯著定製表單輸入。

您可能還注意到 `TextField` 組件中缺少某些本機HTML輸入屬性。 這是故意的。 該組件負責處理最常用的屬性，然後由用戶使用以下演示中顯示的底層組件。 如果你想避免一些樣板，你仍然可以使用 `inputProps` （和 `InputProps` `InputLabelProps` 屬性）。

{{“demo”：“pages / demos / text-fields / ComposedTextField.js”}}

## 輸入

{{“demo”：“pages / demos / text-fields / Inputs.js”}}

## 佈局

`的TextField`， `FormControl` 允許的規範 `餘量` ，以改變輸入的垂直間距。 使用 `none` （默認）不會對 `FormControl`應用邊距，而 `密集` 和 `普通` 將改變其他 種樣式以符合規範。

{{“demo”：“pages / demos / text-fields / TextFieldMargins.js”}}

## 輸入裝飾品

`輸入` 允許提供 `InputAdornment`。 這些可用於向輸入添加前綴，後綴或操作。 例如，您可以使用圖標按鈕隱藏或顯示密碼。

{{“demo”：“pages / demos / text-fields / InputAdornments.js”}}

## 填充輸入裝飾品

{{“demo”：“pages / demos / text-fields / FilledInputAdornments.js”}}

## 概述輸入裝飾

{{“demo”：“pages / demos / text-fields / OutlinedInputAdornments.js”}}

## 格式化輸入

您可以使用第三方庫來格式化輸入。 您必須使用 `inputComponent` 屬性提供 `<input>` 元素的自定義實現。

以下演示使用 [react-text-mask](https://github.com/text-mask/text-mask) 和 [react-number-format](https://github.com/s-yadav/react-number-format) 庫。

{{“demo”：“pages / demos / text-fields / FormattedInputs.js”}}

## 定制輸入

如果您一直在閱讀 [覆蓋文檔頁面](/customization/overrides/) 但是您沒有自信地跳入，這裡是一個如何更改輸入的主要顏色的示例。

{{“demo”：“pages / demos / text-fields / CustomizedInputs.js”}}

## 帶圖標

圖標可以指定為前置或附加。

{{“demo”：“pages / demos / text-fields / InputWithIcon.js”}}

## 限制

輸入標籤“收縮”狀態並不總是正確的。 一旦輸入顯示某些內容，輸入標籤就會縮小。 在某些情況下，我們無法確定“縮小”狀態（數字輸入，日期時間輸入，條帶輸入）。 您可能會注意到重疊。

![收縮](/static/images/text-fields/shrink.png)

要解決此問題，可以強制標籤的“收縮”狀態。

```jsx
<TextField InputLabelProps={{ shrink: true }} />
```

要么

```jsx
<InputLabel shrink>計數</InputLabel>
```