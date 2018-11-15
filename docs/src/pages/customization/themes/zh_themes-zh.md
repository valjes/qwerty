# 主題

<p class="description">使用您的主題自定義Material-UI。 您可以更改顏色，排版等等。</p>

主題指定組件的顏色，表面的暗度，陰影的級別，墨水元素的適當​​不透明度等。

主題可讓您為應用程序應用一致的音調。它可以讓你 **自定義所有的設計方面** 項目，以滿足您的企業或品牌的特定需求。

為了提高應用程序之間的一致性，可以選擇明暗主題類型。 默認情況下，組件使用燈光主題類型。

## 主題提供者

如果要自定義主題，則需要使用 `MuiThemeProvider` 組件才能將主題註入到應用程序中。 但是，這是可選的; Material-UI組件帶有默認主題。

`MuiThemeProvider` 依賴於React的上下文功能將主題傳遞給組件，因此您需要確保 `MuiThemeProvider` 是您嘗試自定義的組件的父級。 您可以了解更多有關這 [API部分](#muithemeprovider)。

## 主題配置變量

更改主題配置變量是將Material-UI與您的需求相匹配的最有效方法。 以下部分介紹了最重要的主題變量：

- [調色板](#palette)
- [類型（淺色/深色主題）](#type-light-dark-theme-)
- [活版印刷](#typography)
- [其他變量](#other-variables)
- [自定義變量](#custom-variables)

### 調色板

#### 意向

顏色意圖是將調色板映射到應用程序中的給定意圖。

該主題揭示了以下顏色意圖：

- primary - 用於表示用戶的主要界面元素。
- secondary - 用於表示用戶的輔助界面元素。
- error - 用於表示用戶應該知道的界面元素。

默認調色板使用前綴為 `A` （`A200`等）的陰影作為次要意圖，使用未加前綴的陰影表示其他意圖。

如果您想了解更多的顏色，你可以檢查出 [顏色項](/style/color/)。

#### 定制調色板

您可以通過在主題中包含 `調色板` 對象來覆蓋默認調色板值。

如果任何的 [`palette.primary`](/customization/default-theme/?expend-path=$.palette.primary)， [`palette.secondary`](/customization/default-theme/?expend-path=$.palette.secondary) 或 [`palette.error`](/customization/default-theme/?expend-path=$.palette.error) 提供的意圖'對象，它們將取代的默認值。

意圖值可以是 [顏色](/style/color/) 對象，也可以是具有以下一個或多個鍵的對象：

```js
interface PaletteIntention {
  light？：string;
  主要：字符串;
  黑暗？：字符串;
  contrastText？：string;
};
```

**使用顏色對象**

自定義意圖的最簡單方法是導入一個或多個提供的顏色並將其應用於調色板意圖：

```js
從'@ material-ui / core / styles'導入 { createMuiTheme } ;
從'@ material-ui / core / colors / blue'導入藍色;

const的主題= createMuiTheme（{
  調色板： {
    primary: blue,
  }，
}）;
```

如果意圖鍵接收到顏色對象，如上例所示，則使用以下映射來填充所需的鍵：

```js
調色板：{
  初級：{
    光：palette.primary[300]，
    主：palette.primary[500]，
    黑暗：palette.primary[700]，
    contrastText：getContrastText（palette.primary[500]），
  }，
  二次：{
    光：palette.secondary.A200，
    主：palette.secondary.A400，
    黑暗：palette.secondary.A700，
    contrastText：getContrastText（palette.secondary.A400），
  }，
  錯誤：{
    光：調色板。錯誤[300]，
    主：palette.error[500]，
    黑暗：palette.error[700]，
    contrastText：getContrastText（palette.error[500]），
  }，
}，
```

此示例說明瞭如何重新創建默認調色板值：

```js
從'@ material-ui / core / styles'導入 { createMuiTheme } ;
從'@ material-ui / core / colors / indigo'導入indigo;
從'@ material-ui / core / colors / pink'導入粉紅色;
從'@ material-ui / core / colors / red'導入紅色;

//以下所有鍵都是可選的。
//我們盡力提供一個很好的默認值。
const theme = createMuiTheme（{
  palette：{
    primary：indigo，
    secondary：pink，
    error：red，
    //由`getContrastText（）`使用，以最大化背景和
    //文本之間的對比度。
    contrastThreshold：3，
    //用於一個顏色的亮度由大約偏移
    //兩個索引其色調調色板內。
    //例如，從紅色500轉換到紅色300或紅色700。
    tonalOffset：0.2，
  }，
}）;
```

**直接提供顏色**

如果您希望提供更多自定義顏色，您可以創建自己的顏色對象，也可以直接為意圖的部分或全部鍵提供顏色：

```js
從'@ material-ui / core / styles'導入 { createMuiTheme } ;

const theme = createMuiTheme（{
  palette：{
    primary：{
      // light：將從palette.primary.main計算，
      main：'＃ff4400'，
      // dark：將從palette.primary計算.main，
      // contrastText：將被計算為與palette.primary.main
    }對比，
    次要：{
      light：'＃0066ff'，
      main：'＃0044ff'，
      // dark：將被計算來自palette.secondary.main，
      contrastText：'＃ffcc00'，
    }，
    //錯誤：將使用默認顏色
  }，
}）;
```

如在上面的示例中，如果意圖對象使用任何的包含自定義顏色 `主`， `光`， `暗` 或 `contrastText` 鍵，這些地圖如下：

- 如果省略 `暗` 和/或 `亮` 鍵，則根據 `tonalOffset` 值從 `主`計算它們的值。

- 如果省略 `contrastText` ，則根據`contrastThreshold` 值計算其值以與 `main`對比。

`tononalOffset` 和 `contrastThreshold` 值都可以根據需要進行定制。 `tonalOffset` 較高值將使 `light` 計算值更亮，而 `dark` 更暗。 `對比度閾值` 較高值增加了背景顏色被認為是亮的點，並且給出了暗 `對比度文本`。

請注意， `contrastThreshold` 遵循非線性曲線。

#### 例

{{“demo”：“pages / customization / themes / Palette.js”}}

#### 顏色工具

需要靈感？ Material Design團隊已經構建了一個非常棒的 [調色板配置工具](/style/color/#color-tool) 來幫助您。

### 類型（淺色/深色主題）

您可以通過將 `類型` 設置為 `暗`來使主題變暗。 雖然它只是單個屬性值更改，但在內部它會修改以下鍵的值：

- `palette.text`
- `palette.divider`
- `palette.background`
- `palette.action`

```js
常量主題= createMuiTheme（{
  調色板： {
    type: 'dark',
  }，
}）;
```

{{“demo”：“pages / customization / themes / DarkTheme.js”，“hideEditButton”：true}}

### 活版印刷

一次太多的類型大小和样式會破壞任何佈局。 主題提供了 **有限集合型尺寸的** 與佈局網格沿一起很好地工作。 這些尺寸用於各個組件。

請查看以下有關更改默認值的示例，例如字體系列。 如果您想了解有關排版的更多信息，可以查看 [排版部分](/style/typography/)。

{{“demo”：“pages / customization / themes / TypographyTheme.js”}}

### 排版 - 字​​體系列

```js
const theme = createMuiTheme（{
  typography：{
    //使用系統字體而不是默認的Roboto字體。
    fontFamily中：[
      ' -蘋果系統'，
      'BlinkMacSystemFont'，
      “'的Segoe UI”'，
      '的Roboto'，
      '“Helvetica Neue字體”'，
      'Arial字體'，
      '無襯線'，
      '“Apple Color Emoji”'，
      '“Segoe UI Emoji”'，
      '“Segoe UI Symbol”'，
    ] .join（'，'），
  }，
}）;
```

### 排版 - 字​​體大小

Material-UI使用 `rem` 單位作為字體大小。 瀏覽器 `<html>` 元素默認字體大小為 `16px`，但瀏覽器可以選擇更改此值，因此 `rem` 單位允許我們適應用戶的設置，從而帶來更好的用戶體驗。 用戶可以出於各種原因更改字體大小設置，從視力不佳到為大小和觀看距離差異很大的設備選擇最佳設置。

要更改Material-UI的字體大小，您可以提供 `fontSize` 屬性。 默認值為 `14px`。

```js
const theme = createMuiTheme（{
  typography：{
    //在日語中，字符通常較大。
    fontSize的：12，
  }，
}）;
```

瀏覽器計算出的字體大小遵循以下數學公式：

![字體大小](/static/images/font-size.gif) <!-- https://latex.codecogs.com/gif.latex?computed&space;=&space;specification&space;\frac{typography.fontSize}{14}&space;\frac{html&space;font&space;size}{typography.htmlFontSize} -->

### 排版 - HTML字體大小

您可能想要更改 `<html>` 元素的默認字體大小。 例如，使用 [10px簡化時](https://www.sitepoint.com/understanding-and-using-rem-units-in-css/)。 我們為這個用例提供了一個 `htmlFontSize` 主題屬性。 它告訴Material-UI `<html>` 元素的字體大小是多少。 它用於調整 `rem` 值，因此計算出的字體大小始終與規範匹配。

```js
const theme = createMuiTheme（{
  typography：{
    //告訴Material-UI html元素的字體大小是什麼。
    htmlFontSize：10，
  }，
}）;
```

```css
html {
  字體大小：62.5％; / * 62.5％的16px = 10px * /
}
```

*您需要在此頁面的html元素上應用上述CSS，以查看正確呈現的以下演示*

{{“demo”：“pages / customization / themes / FontSizeTheme.js”}}

### 其他變量

除了調色板，暗色和淺色類型以及排版外，主題還通過提供更多默認值（例如斷點，陰影，過渡等）來規範化實現。 您可以查看 [默認主題部分](/customization/default-theme/) 以完整查看默認主題。

### 自定義變量

使用Material-UI的 [樣式解決方案](/customization/css-in-js/) 和您自己的組件時，您還可以利用主題。 可以方便地向主題添加其他變量，以便您可以在任何地方使用它們。 例如：

{{“demo”：“pages / customization / themes / CustomStyles.js”}}

## 自定義組件類型的所有實例

### CSS

當配置變量不夠強大時，您可以利用 `主題` 的 `覆蓋` 鍵來潛在地將Material-UI注入的每個 **樣式** 更改為DOM。 這是一個非常強大的功能。

```js
const theme = createMuiTheme（{
  覆蓋：{
    MuiButton：{//組件的名稱⚛️/樣式表
      root：{//規則的名稱
        顏色：'white'，//一些CSS
      }，
    }，
  }，
}）;
```

{{“demo”：“pages / customization / themes / OverridesCss.js”}}

每個組件的這些自定義點列表記錄在 **Component API** 部分下。 例如，您可以查看 [按鈕](/api/button/#css-api)。 或者，您可以隨時查看 [實現](https://github.com/mui-org/material-ui/blob/master/packages/material-ui/src/Button/Button.js)。

### 屬性

您還可以在組件類型的所有實例上應用屬性。 我們在這個用例的 `主題` 公開了一個 `道具` 鍵。

```js
常量主題= createMuiTheme（{
  道具：{
    //組件⚛️的名稱
    MuiButtonBase：{
      //屬性申請
      disableRipple：真，//沒有更多的波紋，對整個應用 
    }，
  } ，
}）;
```

{{“demo”：“pages / customization / themes / OverridesProperties.js”}}

## 訪問組件中的主題

您可能需要訪問React組件中的主題變量。 假設您要顯示主色的值，可以使用 `withTheme（）` 高階組件來執行此操作。 這是一個例子：

{{“demo”：“pages / customization / themes / WithTheme.js”}}

## 嵌套主題

主題解決方案非常靈活，因為您可以嵌套多個主題提供程序。 在處理具有彼此明顯外觀的應用程序的不同區域時，這非常有用。

{{“demo”：“pages / customization / themes / Nested.js”}}

#### 關於表現的說明

嵌套 `MuiThemeProvider` 組件的性能影響與JSS在幕後的工作相關聯。 要理解的要點是我們使用以下元組 `（樣式，主題）`緩存注入的CSS。

- `主題`：如果在每個渲染中提供新主題，則將計算並註入新的CSS對象。 對於UI一致性和性能，最好渲染有限數量的主題對象。
- `樣式`：樣式對象越大，需要的工作量越多。

## API

### `MuiThemeProvider`

該組件採用 `主題` 屬性，並且由於React上下文，使得 `主題` 在React樹下可用。 它最好應在組件樹</strong>的根處使用 **。</p> 

你可以看到完整的屬性API [這個專用頁面](/api/mui-theme-provider/)。

#### 例子

```jsx
從'react'中導入React;
從'react-dom'導入 { render } ;
從'@ material-ui / core / styles'導入 { MuiThemeProvider, createMuiTheme } ;
從'./Root'導入Root;

const theme = createMuiTheme（）;

功能App（）{
  return（
    <MuiThemeProvider theme={theme}>
      <Root />
    </MuiThemeProvider>
  ）;
}

render（<App />，document.querySelector（'＃app'））;
```

### `createMuiTheme（options）=> 主題`

根據收到的選項生成主題。

#### 參數

1. `選項` （*對象*）：採用不完整的主題對象並添加缺少的部分。

#### 返回

`主題` （*對象*）：一個完整的，隨時可用的主題對象。

#### 例子

```js
從'@ material-ui / core / styles'導入 { createMuiTheme } ;
從'@ material-ui / core / colors / purple'導入紫色;
從'@ material-ui / core / colors / green'導入綠色;

const的主題= createMuiTheme（{
  調色板： {
    primary: purple,
    secondary: green,
  }，
  的狀態： {
    danger: 'orange',
  }，
}）;
```

### `withTheme（）（Component）=> Component`

提供 `主題` 像作為輸入組件的屬性，以便可以在render方法中使用它。

#### 參數

1. `組件`：將被包裝的組件。

#### 返回

`組件`：創建新組件。

#### 例子

```js
從'@ material-ui / core / styles'導入 { withTheme } ;

函數MyComponent（props）{
  return <div>{props.theme.direction}</div>;
}

導出默認withTheme（）（MyComponent）;
```