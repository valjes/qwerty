---
title: Divider React組件
components: 分頻器
---
# 分頻器

<p class="description">分隔符是一條細線，用於對列表和佈局中的內容進行分組。</p>

[分隔符](https://material.io/design/components/dividers.html) 將單獨的內容分成清晰的組。

## 列出分隔符

默認情況下，分隔符呈現為 `<hr>`。 您可以使用 `ListItem` 組件上的 `divider` 屬性來保存渲染此DOM元素。

{{“demo”：“pages / demos / dividers / ListDividers.js”}}

## 插入分隔符

以下示例演示了 `inset` 屬性。 我們需要確保將 `Divider` 渲染為 `li` 以匹配HTML5規範。 該示例顯示了實現此目的的兩種方法。

{{“demo”：“pages / demos / dividers / InsetDividers.js”}}