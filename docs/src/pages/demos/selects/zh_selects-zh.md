---
title: 選擇React組件
components: 選擇，NativeSelect
---
# 選擇

<p class="description">選擇組件用於從選項列表中收集用戶提供的信息。</p>

## 簡單選擇

菜單位於其發光元件上方，使得當前選擇的菜單項出現在發光元件的頂部。

{{“demo”：“pages / demos / choices / SimpleSelect.js”}}

## 原生選擇

由於可以使用平台的原生選擇在移動設備上改進用戶體驗，因此我們允許這樣的模式。

{{“demo”：“pages / demos / choices / NativeSelects.js”}}

## 多選

`選擇` 組件可以處理多個選擇。 它啟用 `多重` 屬性。

與單個選擇一樣，您可以通過在 `onChange` 回調中訪問 `event.target.value` 來提取新值。 它總是一個陣列。

{{“demo”：“pages / demos / choices / MultipleSelect.js”}}

## 用對話框

雖然材料設計規範不鼓勵它，但您可以在對話框中使用選擇。

{{“demo”：“pages / demos / choices / DialogSelect.js”}}

## 文字字段

`TextField` 包裝器組件是一個完整的表單控件，包括標籤，輸入和幫助文本。 您可以在本節</a>找到選擇模式 的示例。</p> 

## 受控打開選擇

{{“demo”：“pages / demos / choices / ControlledOpenSelect.js”}}