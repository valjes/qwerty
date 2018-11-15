---
components: 圖標，SvgIcon
---
# 圖標

<p class="description">使用Material-UI使用圖標的指導和建議。</p>

[系統圖標](https://material.io/design/iconography/system-icons.html) 或UI圖標，表示命令，文件，設備或目錄。 系統圖標還用於表示垃圾，打印和保存等常見操作，通常可在應用欄，工具欄，按鈕和列表中找到。 Google提供了一組符合這些指南的 [素材圖標](https://material.io/tools/icons/?style=baseline)。

Material-UI提供兩個組件來渲染系統圖標： `SvgIcon` 用於渲染SVG路徑， `Icon` 用於渲染字體圖標。

## SVG圖標

`SvgIcon` 組件將SVG `路徑` 元素作為其子元素並將其轉換為顯示路徑的React組件，並允許對圖標進行樣式化並響應鼠標事件。 SVG元素應縮放為24x24px視口。

生成的圖標可以按原樣使用，也可以作為其他使用圖標的Material-UI組件的子項包含在內。 默認情況下，Icon將繼承當前文本顏色。 可選地，可以設置使用的主題顏色屬性中的一個圖標顏色： `初級`， `二次`， `的動作`， `錯誤` & `禁用`。

{{“demo”：“pages / style / icons / SvgIcons.js”}}

### SVG材料圖標

擁有實現自定義圖標所需的構建塊很有意思，但預設呢？ 我們提供了一個單獨的npm包， [@ material-ui / icons](https://www.npmjs.com/package/@material-ui/icons)，其中包括轉換為 `SvgIcon` 組件的1,000多個官方 [Material icon](https://material.io/tools/icons/?style=baseline)。

<a href="https://material.io/tools/icons/?icon=3d_rotation&style=baseline">
  <img src="/static/images/icons/icons.png" alt="官方材料圖標" style="width: 566px" />
</a>

#### 用法

您可以使用 [material.io/tools/icons](https://material.io/tools/icons/?style=baseline) 查找特定圖標。 導入圖標時，請記住圖標的名稱為 `PascalCase`，例如： - [`刪除`](https://material.io/tools/icons/?icon=delete&style=baseline) 暴露為 `@ material-ui / icons /刪除` - [`永久刪除`](https://material.io/tools/icons/?icon=delete_forever&style=baseline) 暴露作為 `@ material -ui / icons / DeleteForever`

對於 *“主題”* 圖標，將主題名稱附加到圖標名稱。 例如，使用 - The Outlined [`刪除`](https://material.io/tools/icons/?icon=delete&style=outline) 圖標顯示為 `@ material-ui / icons / DeleteOutlined` - Rounded [`刪除`](https://material.io/tools/icons/?icon=delete&style=rounded) 圖標顯示為 `@ material-ui / icons / DeleteRounded` -雙音 [`刪除`](https://material.io/tools/icons/?icon=delete&style=twotone) 圖標顯示為 `@ material -ui / icons / DeleteTwoTone` - 夏普 [`刪除`](https://material.io/tools/icons/?icon=delete&style=sharp) 圖標顯示為 `@ material-ui / icons / DeleteSharp`

此規則有三個例外： - [`3d_rotation`](https://material.io/tools/icons/?icon=3d_rotation&style=baseline) 暴露為 `@ material-ui / icons / ThreeDRotation` - [`4k`](https://material.io/tools/icons/?icon=4k&style=baseline) 暴露為 `@ material-ui / icons / FourK` - [`360`](https://material.io/tools/icons/?icon=360&style=baseline) 暴露為 `@ material-ui / icons / ThreeSixty`

{{“demo”：“pages / style / icons / SvgMaterialIcons.js”}}

#### 進口

- 如果您的環境不支持樹搖動，在 **推薦** 導入的圖標方法如下：

```jsx
從'@ material-ui / icons / AccessAlarm'導入AccessAlarmIcon;
從'@ material-ui / icons / ThreeDRotation'導入ThreeDRotation;
```

- 如果您的環境支持樹搖動，您也可以通過以下方式導入圖標：

```jsx
從'@ material-ui / icons'導入 { AccessAlarm, ThreeDRotation };
```

注意：以這種方式導入命名導出將導致項目中包含每個圖標</em> *代碼，因此除非您配置 [樹抖動](https://webpack.js.org/guides/tree-shaking/)否則不建議這樣做。 它還可能影響熱模塊重新加載性能。</p> 

### 更多SVG圖標

正在尋找更多SVG圖標？ 有很多項目，但 [https://materialdesignicons.com](https://materialdesignicons.com/) 提供超過2,000個官方和社區提供的圖標。 [mdi-material-ui](https://github.com/TeamWertarbyte/mdi-material-ui) 這些圖標打包為Material-UI SvgIcons，其方式與 [@ material-ui / icons](https://www.npmjs.com/package/@material-ui/icons) 對官方圖標的處理方式大致相同。

## 字體圖標

`Icon` 組件將顯示支持連字的任何圖標字體的圖標。 作為先決條件，您必須包含一個，例如項目中的 [Material icon font](http://google.github.io/material-design-icons/#icon-font-for-the-web) ，例如，通過Google Web Fonts：

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

`圖標` 將為“材質”圖標字體設置正確的類名。 對於其他字體，您必須使用Icon組件的 `className` 屬性提供類名。

要使用圖標，只需將圖標名稱（字體連字）與 `Icon` 組件包裝在一起，例如：

```jsx
<Icon>星</Icon>
```

默認情況下，Icon將繼承當前文本顏色。 可選地，可以設置使用的主題顏色屬性中的一個圖標顏色： `初級`， `二次`， `的動作`， `錯誤` & `禁用`。

### 字體材料圖標

{{“demo”：“pages / style / icons / Icons.js”}}

### 字體真棒

[Font Awesome](https://fontawesome.com/icons) 可與 `Icon` 組件一起使用，如下所示：

{{“demo”：“pages / style / icons / FontAwesome.js”，“hideEditButton”：true}}

## 字體vs SVG。 使用哪種方法？

兩種方法都可以正常工作，但是，存在一些細微差別，特別是在性能和​​渲染質量方面。 只要有可能，SVG是首選，因為它允許代碼分割，支持更多圖標，渲染速度更快更好。

有關更多詳細信息，您可以查看 [為什麼GitHub將](https://blog.github.com/2016-02-22-delivering-octicons-with-svg/) 從字體圖標遷移到SVG圖標。

## 無障礙

圖標可以傳達各種有意義的信息，因此重要的是它們可以覆蓋盡可能多的人。 您需要考慮兩種用例： - **裝飾圖標** 僅用於視覺或品牌強化。 如果將它們從頁面中刪除，用戶仍然可以理解並能夠使用您的頁面。 - **語義圖標** 是您用來傳達意義的，而不僅僅是純粹的裝飾。 這包括它們旁邊沒有文本的圖標用作交互式控件 - 按鈕，表單元素，切換等。

### 裝飾SVG圖標

如果您的圖標純粹是裝飾性的，那麼您已經完成了！ 我們添加 `aria-hidden = true` 屬性，以便您的圖標可以正確訪問（不可見）。

### 語義SVG圖標

如果您的圖標具有語義含義，那麼您需要做的就是輸入 `titleAccess =“含義”` 屬性。 我們添加 `role =“img”` 屬性和 `<title>` 元素，以便您的圖標可以正常訪問。

對於可聚焦的交互式元素，例如與圖標按鈕一起使用時，您可以使用 `aria-label` 屬性：

```jsx
從'@ material-ui / core / IconButton'導入IconButton;
從'@ material-ui / core / SvgIcon'導入SvgIcon;

// ......

<IconButton aria-label="Delete">
  <SvgIcon>
    <path d="M20 12l-1.41-1.41L13 16.17V4h-2v12.17l-5.58-5.59L4 12l8 8 8-8z" />
  </SvgIcon>
</IconButton>
```

### 裝飾字體圖標

如果您的圖標純粹是裝飾性的，那麼您已經完成了！ 我們添加 `aria-hidden = true` 屬性，以便您的圖標可以正確訪問（不可見）。

### 語義字體圖標

如果您的圖標具有語義含義，則需要提供僅對輔助技術可見的文本替代方法。

```jsx
從'@ material-ui / core / Icon'導入圖標;
從'@ material-ui / core / Typography'導入排版;

// ......

<Icon>add_circle</Icon>
<Typography variant="srOnly">創建用戶</Typography>
```

### 參考

- https://developer.paciellogroup.com/blog/2013/12/using-aria-enhance-svg-accessibility/