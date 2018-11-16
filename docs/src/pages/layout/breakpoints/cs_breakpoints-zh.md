# 斷點

<p class="description">斷點是具有特定佈局要求的預定屏幕尺寸的範圍。</p>

為了獲得最佳的用戶體驗，材料設計界面需要能夠在各種斷點處調整其佈局。 Material-UI使用原始 [規範](https://material.io/design/layout/responsive-layout-grid.html#breakpoints)的 **簡化** 實現。

與每個斷點比賽 *固定* 屏幕寬度：

- **xs**，extra-small：0px或更大
- **sm**，小：600px或更大
- **md**，中等：960px或更大
- **lg**，大：1280px或更大
- **xl**，超大：1920px或更大

始終可以自定義這些值。 您將在主題中找到它們，在 [`breakpoints.values`](/customization/default-theme/?expend-path=$.breakpoints.values) 像中。

斷點在內部用於各種組件以使其響應，但您也可以利用它們通過 [Grid](/layout/grid/) 和 [Hidden](/layout/hidden/) 組件控制應用程序的佈局。

## 媒體查詢

CSS媒體查詢是使您的UI響應的慣用方法。 我們提供了一些 [CSS-in-JS](/customization/css-in-js/) 助手。

在下面的演示中，我們根據屏幕寬度更改背景顏色（紅色，藍色 & 綠色）。

{{“demo”：“pages / layout / breakpoints / MediaQuery.js”}}

## withWidth（）

有時，使用CSS是不夠的。 您可能希望在JavaScript中基於斷點值更改React呈現樹。 我們為此用例提供了一個 `withWidth（）` 高階組件。

```js
從'@ material-ui / core / withWidth'導入withWidth;

函數MyComponent的（道具）{
  返回 <div>{`電流寬度： ${props.width}`}</div>;
}

export default withWidth（）（MyComponent）;
```

在下面的演示中，我們改變呈現的DOM元素（*EM*， <u>ü</u>，~~德爾~~ & 基於屏幕寬度跨度）。

{{“demo”：“pages / layout / breakpoints / WithWidth.js”}}

⚠️ `withWidth（）` 的服務器端渲染支持有限。

### 渲染道具

在某些情況下，您可以使用高階組件進行屬性名稱衝突。 為避免此問題，您可以使用 [渲染道具](https://reactjs.org/docs/render-props.html) 模式，如下面的演示。

```js
從'@ material-ui / core / Typography'導入排版;
從'recompose / toRenderProps'導入toRenderProps;

const WithWidth = toRenderProps（withWidth（））;

出口缺省功能MyComponent的（）{
  返回（
    <WithWidth>
      {（{ width }）=> <div>{`電流寬度： ${width}`}</div>}
    </WithWidth>
  ）;
}
```

{{“demo”：“pages / layout / breakpoints / RenderPropsWithWidth.js”}}

## API

### `withWidth（[options]）=> 個高階分量`

注入 `寬度` 屬性。 它不會修改傳遞給它的組件;相反，它返回一個新組件。 此 `寬度` 斷點屬性與當前屏幕寬度匹配。 它可以是以下斷點之一：

```ts
類型Breakpoint ='xs'| 'sm'| 'md'| 'lg'| 'XL';
```

一些可能有趣的實現細節：

- 它轉發 *非React靜態* 屬性，因此這個HOC更“透明”。 例如，它可以用於定義一個 `getInitialProps（）` 靜態方法（next.js）。

#### 參數

1. `選項` （*對象* [optional]）： 
    - `options.withTheme` （*布爾值* [optional]）：默認值為 `false`。 將 `主題` 對像作為屬性提供給組件。
    - `options.noSSR` （*布爾值* [optional]）：默認值為 `false`。 為了執行服務器端渲染協調，我們需要渲染兩次。 第一次沒有任何東西，第二次與孩子們在一起。 這種雙遍渲染週期有一個缺點。 用戶界面可能會閃爍。 如果不進行服務器端渲染，可以將此標誌設置為 `true`。
    - `options.initialWidth` （*Breakpoint* [optional]）：由於 `window.innerWidth` 在服務器上不可用，我們默認在第一次安裝期間渲染一個空組件。 在某些情況下，您可能希望使用啟發式來近似客戶端瀏覽器屏幕寬度的屏幕寬度。 例如，您可以使用用戶代理或客戶端提示。 https://caniuse.com/#search=client%20hint，我們還可以使用主題上的 [`自定義屬性`](/customization/themes/#properties) 全局設置初始寬度。 為了設置initialWidth，我們需要傳遞一個具有以下形狀的自定義屬性：

```js
常量主題= createMuiTheme（{
  道具：{
    // withWidth部件⚛️
    MuiWithWidth：{
      //初始寬度屬性
      initialWidth：“LG'，//斷點被全局地設置 
    }，
  }，
}）;
```

- `options.resizeInterval` （*Number* [optional]）：默認為166，對應於60 Hz的10幀。 響應屏幕調整大小事件之前等待的毫秒數。

#### 返回

`高階組件`：應該用於包裝組件。

#### 例子

```jsx
從'@ material-ui / core / withWidth'導入withWidth， { isWidthUp } ;

類MyComponent擴展React.Component {
  render（）{
    if（isWidthUp（'sm'，this.props.width））{
      return <span />
    }

    return <div />;
  }
}

導出默認值withWidth（）（MyComponent）;
```

### `theme.breakpoints.up（key）=> 媒體查詢`

#### 參數

1. `鍵` （*字符串* | *號*）：斷點密鑰（`XS`， `SM`等）或在像素的屏幕寬度數。

#### 返回

`媒體查詢`：準備與JSS一起使用的媒體查詢字符串。

#### 例子

```js
const styles = theme => （{
  root：{
    backgroundColor：'blue'，
    // Match [md，∞[
    // [960px，∞[
    [theme.breakpoints.up（'md'）]： {
      backgroundColor: 'red',
    }，
  }，
}）;
```

### `theme.breakpoints.down（key）=> 媒體查詢`

#### 參數

1. `鍵` （*字符串* | *號*）：斷點密鑰（`XS`， `SM`等）或在像素的屏幕寬度數。

#### 返回

`媒體查詢`：準備與JSS一起使用的媒體查詢字符串。

#### 例子

```js
const styles = theme => （{
  root：{
    backgroundColor：'blue'，
    // Match [0，md + 1 [
    // [0，lg [
    // [0,1280px [
    [主題。 breakpoints.down（'MD'）〕： {
      backgroundColor: 'red',
    }，
  }，
}）;
```

### `theme.breakpoints.only（key）=> 媒體查詢`

#### 參數

1. `鍵` （*字符串*）：斷點鍵（`XS`， `SM`等）。

#### 返回

`媒體查詢`：準備與JSS一起使用的媒體查詢字符串。

#### 例子

```js
const styles = theme => （{
  root：{
    backgroundColor：'blue'，
    // Match [md，md + 1 [
    // [md，lg [
    // [960px，1280px [
    [theme。 breakpoints.only（'MD'）〕： {
      backgroundColor: 'red',
    }，
  }，
}）;
```

### `theme.breakpoints.between（start，end）=> 媒體查詢`

#### 參數

1. `開始` （*字符串*）：斷點鍵（`XS`， `SM`等）。
2. `端` （*字符串*）：斷點鍵（`XS`， `SM`等）。

#### 返回

`媒體查詢`：準備與JSS一起使用的媒體查詢字符串。

#### 例子

```js
const styles = theme => （{
  root：{
    backgroundColor：'blue'，
    // Match [sm，md + 1 [
    // [sm，lg [
    // [600px，1280px [
    [主題。 breakpoints.between（'SM'，'MD'）〕： {
      backgroundColor: 'red',
    }，
  }，
}）;
```