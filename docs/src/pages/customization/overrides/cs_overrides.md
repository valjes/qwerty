# 覆蓋

<p class="description">由於組件可以在不同的上下文中使用，因此Material-UI支持從最具體到最通用的不同類型的自定義要求。</p>

1. [一次性情況的具體變化](#1--specific-variation-for-a-one-time-situation)
2. [一次性情況的動態變化](#2--dynamic-variation-for-a-one-time-situation)
3. [在不同環境中重複使用的組件](#3--specific-variation-of-a-component) 特定變體
4. [材料設計變體](#4--material-design-variations) 例如按鈕組件
5. [全球主題變化](#5--global-theme-variation)

## 1。 一次性情況的具體變化

您可能需要在某些特定情況下更改組件的樣式，您可以使用以下解決方案：

### 覆蓋類名

覆蓋組件樣式的第一種方法是使用 **類名**。 每個組件都提供一個 `className` 屬性，該屬性始終應用於根元素。

在這個例子中，我們使用的是 [`withStyles（）`](/customization/css-in-js/#withstyles-styles-options-higher-order-component) 高階 組分注入自定義風格到DOM，並且對類名傳遞給 `類名` 通過組件 及其 `類` 道具。 您可以選擇任何其他造型的解決方案，甚至普通的CSS創建的樣式，但一定要 考慮 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如CSS注入DOM 通過材料的UI樣式組件具有最高的特異性可能因為 `<link>` 被注入 `<head />` 的底部 ，以確保組件始終正確呈現。

{{“demo”：“pages / customization / overrides / ClassNames.js”}}

### 覆蓋類

當 `className` 屬性不夠，並且您需要訪問更深層元素時，您可以利用 `類` 屬性來自定義Material-UI為給定組件注入的所有CSS。 每個 組件的類列表記錄在 **Component API** 部分中。 例如，您可以查看 [Button CSS API](/api/button/#css-api)。 或者，您可以隨時查看 [實現細節](https://github.com/mui-org/material-ui/blob/master/packages/material-ui/src/Button/Button.js)。

這個例子也使用 `withStyles（）` （見上文），但是這裡， `ClassesNesting` 使用 `Button`的 `類` prop到 提供了一個對象，它映射了 **個類的名稱以覆蓋** （鍵）到要應用</strong> （值）的 **CSS類名。 組件的現有類將繼續注入，因此只需要提供要添加或覆蓋的特定樣式 。</p> 

請注意，除按鈕樣式外，按鈕標籤的大小寫也已更改：

{{“demo”：“pages / customization / overrides / ClassesNesting.js”}}

#### 速記

上面的代碼示例可以通過使用縮合 **相同的CSS API** 作為子組件。 在此示例中， `withStyles（）` 高階分量正在註入由 [`Button` 組件](/api/button/#css-api)使用的 `類` 屬性。

```jsx
常量StyledButton = withStyles（{
  根：{
    背景：'線性梯度（45deg，＃FE6B8B 30％，＃FF8E53 90％）'，
    borderRadius：3，
    邊界：0，
    色：“白色”，
    高度：48，
    填充：'0 30PX'，
    boxShadow：'0 3PX 5px的2px的RGBA（255，105，135，0.3）'，
  }，
  標籤： {
    textTransform: 'capitalize',
  }，
}）（按鈕）;
```

{{“demo”：“pages / customization / overrides / ClassesShorthand.js”}}

#### 內部狀態

除了訪問嵌套元素之外， `類` 屬性還可用於自定義Material-UI組件的內部狀態。 組件內部狀態，如 `：懸停`， `：焦點`， `禁用` 和 `中選擇`，都具有較高的CSS特異性樣式。 [特異性是應用於給定CSS聲明的權重](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)。 為了覆蓋組件內部狀態， **需要增加特異性**。 以下是 `禁用` 狀態和按鈕組件的示例：

```css
.classes-state-root {
  / * ... * /
}
.classes-state-root.disabled {
  color：white;
}
```

```jsx
<br />&lt;Button
  disabled
  classes={{
    root: 'classes-state-root',
    disabled: 'disabled', }
  }
&gt;

```

#### 使用 `$ruleName` 引用同一樣式表中的本地規則

[jss-nested](https://github.com/cssinjs/jss-nested) 插件（默認情況下可用）可以使增加特異性的過程更容易。

```js
常量樣式= {
  根：{
    '&$disabled'： {
      color: 'white',
    }，
  }，
  禁用：{}，
};
```

編譯為：

```css
.root-x.disable-x {
  顏色：白色;
}
```

{{“demo”：“pages / customization / overrides / ClassesState.js”}}

### 覆蓋內聯樣式

覆蓋組件樣式的第二種方法是使用 **內聯樣式** 方法。 每個組件都提供 `style` 屬性。 這些屬性始終應用於根元素。

您不必擔心CSS特性，因為內聯樣式優先於常規CSS。

{{“demo”：“pages / customization / overrides / InlineStyle.js”}}

[我什麼時候應該使用內聯式vs類？](/getting-started/faq/#when-should-i-use-inline-style-vs-classes-)

## 2。 一次性情況的動態變化

您已經學習瞭如何覆蓋前面部分中的Material-UI組件的樣式。 現在，讓我們看看我們如何使這些覆蓋動態化。 我們展示了5種替代方案，每種方案都有其優缺點。

### withStyles屬性支持

```jsx
const styles = {
  button：{
    background：props => props.color，
  }，
};
```

此功能尚未準備好。 它將伴隨： [＃7633](https://github.com/mui-org/material-ui/issues/7633)。

### 班級分支

{{“demo”：“pages / customization / overrides / DynamicClassName.js”}}

### CSS變量

{{“demo”：“pages / customization / overrides / DynamicCSSVariables.js”}}

### 內嵌式

{{“demo”：“pages / customization / overrides / DynamicInlineStyle.js”}}

### 主題嵌套

{{“demo”：“pages / customization / overrides / DynamicThemeNesting.js”}}

## 3。 組件的具體變化

您可能需要創建組件的變體並在不同的上下文中使用它，例如產品頁面上的彩色按鈕，但是您可能希望保留代碼 [*DRY*](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)。

最好的方法是遵循選項1，然後通過導出自定義組件來利用React的組合功能，以便在任何需要的地方使用。

{{“demo”：“pages / customization / overrides / Component.js”，“hideEditButton”：true}}

## 4。 材料設計變化

Material Design規範記錄了某些組件的不同變化，例如按鈕的形狀如何： [文本](https://material.io/design/components/buttons.html#text-button) （以前稱為“平面”）， [包含](https://material.io/design/components/buttons.html#contained-button) （以前稱為“凸起”）， [FAB](https://material.io/design/components/buttons-floating-action-button.html) 及更多。

Material-UI嘗試實現所有這些變體。 請參閱 [支持的組件](/getting-started/supported-components/) 文檔，以了解所有支持的Material Design組件的當前狀態。

## 5。 全球主題變化

### 主題變量

為了提高組件之間的一致性，並整體管理用戶界面外觀，Material-UI提供了一種通過調整 [主題配置變量來應用全局更改的機制](/customization/themes/#theme-configuration-variables)。

### 全局主題覆蓋

是否要自定義 **組件類型的所有實例**？

當配置變量不夠強大時， 可以利用 `主題` 的 `覆蓋` 鍵來潛在地將Material-UI注入的每個樣式更改為DOM。 在文檔的 [主題部分](/customization/themes/#customizing-all-instances-of-a-component-type) 中了解有關它的更多信息。

### 全局CSS覆蓋

您還可以使用CSS自定義組件的所有實例。 我們公開了一個 `dangerouslyUseGlobalCSS` 選項來執行此操作。 在文檔的JS第</a> 部分的 CSS中了解更多相關信息。 它與您自定義Bootstrap的方式非常相似。</p>