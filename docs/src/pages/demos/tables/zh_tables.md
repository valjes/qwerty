---
title: 表格反應組件
components: Table，TableBody，TableCell，TableFooter，TableHead，TablePagination，TableRow，TableSortLabel
---
# 表

<p class="description">數據表顯示數據集。 它們可以完全定制。</p>

[數據表](https://material.io/design/components/data-tables.html) 以易於掃描的方式顯示信息，以便用戶可以查找模式和見解。 它們可以嵌入主要內容中，例如卡片。

數據表可以包括： - 相應的可視化 - 導航 - 用於查詢和操縱數據的工具

包括工具時，應將它們直接放在工作台的上方或下方。

## 結構體

數據表包含頂部的標題行，列出列名，後跟數據行。

如果用戶需要選擇或操作數據，則每行應附有復選框。

對於可訪問性，第一列設置為 `<th>` 元素， `範圍` 為 `“行”`。 這使屏幕閱讀器可以通過它的行和列名來標識單元格的值。

## 簡單的表

一個沒有多餘裝飾的簡單例子。

{{“demo”：“pages / demos / tables / SimpleTable.js”}}

## 排序 & 選擇

此示例演示如何使用 `Checkbox` 和可單擊行進行選擇，並使用自定義 `工具欄`。 它使用 `TableSortLabel` 組件來幫助設置列標題的樣式。

該表已被賦予固定寬度以演示水平滾動。 為了防止分頁控件滾動，TablePagination組件在Table外部使用。 （下面的 ['自定義表分頁操作'示例](#custom-table-pagination-action) 顯示了TableFooter中的分頁。）

{{“demo”：“pages / demos / tables / EnhancedTable.js”}}

## 自定義表分頁操作

`TablePagination` 組件的 `Action` 屬性允許實現 自定義操作。

{{“demo”：“pages / demos / tables / CustomPaginationActionsTable.js”}}

## 定製表

您可以通過覆蓋 `TableCell` 組件的樣式來自定義表的外觀。

{{“demo”：“pages / demos / tables / CustomizedTable.js”}}

## 高級用例

對於更高級的用例，您可以利用： - [dx-react-grid-material-ui](https://devexpress.github.io/devextreme-reactive/react/grid/) Material-UI的數據網格，具有分頁，排序，過濾，分組和編輯功能（[自定義許可證](https://js.devexpress.com/licensing/)）。 - [mui-datatables](https://github.com/gregnb/mui-datatables) 具有過濾，排序，搜索等功能的Material-UI響應數據表。 - [material-table](https://github.com/mbrn/material-table) DataTable基於表組件，具有搜索，過濾，排序等附加功能。 - [mui-virtualized-table](https://github.com/techniq/mui-virtualized-table) 虛擬化材料-UI表。