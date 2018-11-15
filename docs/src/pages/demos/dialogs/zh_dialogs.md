---
title: Dialog React組件
components: Dialog，DialogTitle，DialogContent，DialogContentText，DialogActions，Slide
---
# 對話框

<p class="description">對話框通知用戶任務，可以包含關鍵信息，需要決策或涉及多個任務。</p>

A [對話框](https://material.io/design/components/dialogs.html) 是一種 [模態](/utils/modal/) 窗口，出現在應用程序內容的前面，以提供關鍵信息或要求做出決定。 對話框在出現時禁用所有應用功能，並保留在屏幕上，直到確認，解除或執行必要的操作為止。

對話是故意中斷的，所以應該謹慎使用它們。

## 簡單的對話框

簡單對話框可以提供有關列表項的其他詳細信息或操作。 例如，他們可以顯示頭像，圖標，澄清子文本或正交動作（例如添加帳戶）。

觸摸機制： - 選擇一個選項會立即提交選項並關閉菜單 - 觸摸對話框外部，或按返回，取消操作並關閉對話框

{{“demo”：“pages / demos / dialogs / SimpleDialog.js”}}

## 警報

警報是緊急中斷，需要確認，通知用戶情況。

大多數警報不需要標題。 他們通過以下兩種方式總結了一兩句話的決定： - 提出問題（例如“刪除此對話？”） - 製作與動作按鈕相關的陳述

僅在高風險情況下使用標題欄警報，例如可能丟失連接。 用戶應該能夠僅根據標題和按鈕文本來理解選擇。

如果需要標題：

- 在內容區域中使用明確的問題或陳述以及解釋，例如“擦除USB存儲？”。
- 避免道歉，歧義或問題，例如“警告！”或“你確定嗎？”

{{“demo”：“pages / demos / dialogs / AlertDialog.js”}}

您也可以換出轉換，下一個示例使用 `幻燈片`。

{{“demo”：“pages / demos / dialogs / AlertDialogSlide.js”}}

## 確認對話框

確認對話框要求用戶在提交選項之前明確確認其選擇。 例如，用戶可以收聽多個鈴聲，但只有在觸摸“確定”時才進行最終選擇。

在確認對話框中觸摸“取消”或按“返回”，取消操作，放棄所有更改，然後關閉對話框。

{{“demo”：“pages / demos / dialogs / ConfirmationDialog.js”}}

## 全屏對話框

{{“demo”：“pages / demos / dialogs / FullScreenDialog.js”}}

## 表單對話框

表單對話框允許用戶填寫對話框中的表單域。 例如，如果您的網站提示潛在訂閱者填寫他們的電子郵件地址，他們可以填寫電子郵件字段並觸摸“提交”

{{“demo”：“pages / demos / dialogs / FormDialog.js”}}

## 響應全屏

您可以使用 `withMobileDialog`在 `對話框` 響應全屏顯示對話框。 默認情況下， `withMobileDialog（）（Dialog）` 響應全屏 *或低於* `sm` [屏幕尺寸](/layout/basics/)。 您可以通過傳遞 `斷點` 參數來選擇自己的斷點，例如 `xs` ： `withMobileDialog（{breakpoint: 'xs'}）（Dialog）`。

{{“demo”：“pages / demos / dialogs / ResponsiveDialog.js”}}

## 無障礙

請務必將 `aria-labelledby =“id ...”`（引用模態標題）添加到 `對話框`。 此外，您可以在 `對話框`上使用 `aria-describedby =“id ...”` 屬性給出模態對話框的描述。

## 滾動長內容

當對話框對於用戶的視口或設備變得太長時，它們會滾動。 - `滾動=紙張` 對話框的內容在紙張元素內滾動。 - `scroll = body` 對話框的內容在body元素內滾動。

試試下面的演示來看看我們的意思：

{{“demo”：“pages / demos / dialogs / ScrollDialog.js”}}