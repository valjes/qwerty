# 顏色

<p class="description">通過顏色傳達意義。 開箱即用，您可以訪問Material Design規範中的所有顏色。</p>

[顏色](https://material.io/design/color/) 的材質設計靈感來自大膽的色調，與柔和的環境，深色陰影和明亮的高光並置。

## 色彩系統

Material Design顏色系統可用於創建反映您的品牌或風格的顏色主題。

### 重要條款

#### “調色板”

調色板是顏色的集合，即色調和它們的陰影。 Material-UI提供Material Design準則中的所有顏色。

#### “Hue” & “Shade”

調色板中的單色由諸如“紅色”的色調和諸如“500”的色調組成。 “紅色50”是最淺的紅色（*粉紅色！*），而“紅色900”是最暗的。 此外，大多數色調都帶有“重音”色調，前綴為 `A`。

### 例子

“材質設計”調色板包含主色和強調色，可用於說明或開髮品牌顏色。 他們被設計成彼此和諧地工作。

例如，可以參考互補初級和強調色（例如'紅500' & '紫A200'），如下所示：

```js
從'@ material-ui / core / colors / purple'導入紫色;
從'@ material-ui / core / colors / red'導入紅色;

const primary = red[500]; //＃F44336
const accent = purple ['A200']; //＃E040FB
const accent2 = purple.A200; //＃E040FB（替代方法）
```

## 顏色工具

要使用Material-UI 文檔測試 [material.io/color](https://material.io/design/color/) 顏色方案，只需使用下面的調色板和滑塊選擇顏色即可。 或者，您可以在“主要”和“輔助”文本字段中輸入十六進制值。

{{“demo”：“pages / style / color / ColorTool.js”，“hideHeader”：true}}

顏色樣本中顯示的輸出可以直接粘貼到 [`createMuiTheme（）`](/customization/themes/#createmuitheme-options-theme) 函數中（與 [`MuiThemeProvider`](/customization/themes/#theme-provider)）：

```jsx
從'@ material-ui / core / styles'導入 { createMuiTheme } ;
從'@ material-ui / core / colors / purple'導入紫色;

const的主題= createMuiTheme（{
  調色板：{
    初級：紫，
    次級： {
      main: '#f44336',
    }，
  }，
}）;
```

只需要提供 `主要` 陰影（除非您希望進一步自定義 `燈光` `暗` 或 `contrastText`），因為其他顏色將由 `createMuiTheme（）`計算，如 [主題定制中所述](/customization/themes/#palette) 節。

如果您使用默認的主色調和/或輔助色調，則通過提供顏色對象， `createMuiTheme（）` 將使用材質顏色中適當的陰影，用於主色，淺色和深色。

### 官方色彩工具

Material Design團隊還構建了一個很棒的調色板配置工具： [material.io/tools/color](https://material.io/tools/color/)。 這可以幫助您為UI創建調色板，以及測量任何顏色組合的可訪問性級別。

<a href="https://material.io/tools/color/#!/?view.left=0&view.right=0&primary.color=3F51B5&secondary.color=F44336">
  <img src="/static/images/color/colorTool.png" alt="官方色彩工具" style="width: 574px" />
</a>

輸出可以輸入 `createMuiTheme（）` 函數：

```jsx
從'@ material-ui / core / styles'導入 { createMuiTheme } ;

const theme = createMuiTheme（{
  palette：{
    primary：{
      light：'＃757ce8'，
      main：'＃3f50b5'，
      dark：'＃002884'，
      contrastText：'＃ff'，
    }，
    中學：{
      light：'＃ff7961'，
      main：'＃f44336'，
      dark：'＃ba000d'，
      contrastText：'＃000'，
    }，
  }，
}）;
```

### 社區的工具

- [create-mui-theme](https://react-theming.github.io/create-mui-theme/) 是一個在線工具，用於通過Material Design Color Tool創建Material-UI主題。
- [material-ui-theme-editor](https://in-your-saas.github.io/material-ui-theme-editor/) 通過選擇顏色和進行實時預覽，為Material-UI應用程序生成主題的工具。

## 調色板

此調色板包含主色和強調色，可用於說明或開髮品牌顏色。 他們被設計成彼此和諧地工作。

{{“demo”：“pages / style / color / Color.js”，“hideHeader”：true}}