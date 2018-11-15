---
title: 列出React組件
components: Collapse，Divider，List，ListItem，ListItemAvatar，ListItemIcon，ListItemSecondaryAction，ListItemText，ListSubheader
---
# 清單

<p class="description">列表是文本或圖像的連續垂直索引。</p>

[列表](https://material.io/design/components/lists.html) 是一組連續的文本或圖像。 它們由包含主要和補充操作的項目組成，這些操作由圖標和文本表示。

## 簡單清單

{{“demo”：“pages / demos / lists / SimpleList.js”}}

上一個演示的最後一項顯示瞭如何呈現鏈接：

```jsx
function ListItemLink（props）{
  return <ListItem button component="a" {...props} />;
}

// ...

<ListItemLink href="#simple-list">
  <ListItemText primary="Spam" />
</ListItemLink>
```

您可以按照文檔的第</a> 部分找到帶有React Router的 演示。</p> 

## 文件夾列表

{{“demo”：“pages / demos / lists / FolderList.js”}}

## 插入列表

{{“demo”：“pages / demos / lists / InsetList.js”}}

## 嵌套列表

{{“demo”：“pages / demos / lists / NestedList.js”}}

## 選擇ListItem

{{“demo”：“pages / demos / lists / SelectedListItem.js”}}

## 固定的子標題列表

滾動時，子標題仍然固定在屏幕頂部，直到下一個子標題推離屏幕。

此功能依賴於CSS粘貼定位。 不幸的是它的 [沒有實現](https://caniuse.com/#search=sticky) 所有我們支持的瀏覽器。 不支持時，我們默認為 `disableSticky`。

{{“demo”：“pages / demos / lists / PinnedSubheaderList.js”}}

## 列表控件

### 複選框

複選框可以是主要操作，也可以是次要操作。

該複選框是列表項的主要操作和狀態指示器。 註釋按鈕是輔助操作和單獨的目標。

{{“demo”：“pages / demos / lists / CheckboxList.js”}}

該複選框是列表項的輔助操作和單獨的目標。

{{“demo”：“pages / demos / lists / CheckboxListSecondary.js”}}

### 開關

該開關是輔助操作和單獨的目標。

{{“demo”：“pages / demos / lists / SwitchListSecondary.js”}}

## 互動

下面是一個交互式演示，可讓您探索不同設置的可視結果：

{{“demo”：“pages / demos / lists / InteractiveList.js”}}