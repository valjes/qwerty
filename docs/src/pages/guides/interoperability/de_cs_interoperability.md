# 樣式庫互操作性

<p class="description">雖然使用Material-UI提供的基於JSS的樣式解決方案來設置應用程序樣式很簡單，但可以使用您喜歡的任何樣式解決方案，從純CSS到任意數量的CSS-in-JS庫。</p>

本指南旨在記錄最受歡迎的替代方案， 但您應該發現此處應用的原理可以適用於其他庫。

我們提供了以下樣式解決方案的示例：

- [原始CSS](#raw-css)
- [樣式組件](#styled-components)
- [情感](#emotion)
- [反應情緒](#react-emotion)
- [CSS模塊](#css-modules)
- [全球CSS](#global-css)
- [反應JSS](#react-jss)
- [CSS到MUI webpack Loader](#css-to-mui-webpack-loader)
- [魅力](#glamor)

## 原始CSS

沒什麼特別的，只是簡單的舊CSS。 為什麼重新發明輪子已經工作了幾十年？

**RawCssButton.css**

```css
.button {
  background：linear-gradient（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  border-radius：3px;
  邊界：0;
  色：白色;
  高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135，.3）;
}
```

**RawCssButton.js**

```jsx
從'react'中導入React;
來自'@ material-ui / core / Button'的導入按鈕;

函數RawCssButton（）{
  return（
    <div>
      <Button>
        Material-UI
      </Button>
      <Button className="button">
        Raw CSS
      </Button>
    </div>
  ）;
}

導出默認RawCssButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/vmv2mz9785)

**注意：** JSS在 `<head>`的底部注入其樣式。 如果您不想使用 **！important**標記樣式屬性，則需要更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如演示中所示。

## 樣式組件

![明星](https://img.shields.io/github/stars/styled-components/styled-components.svg?style=social&label=Star) ![NPM](https://img.shields.io/npm/dm/styled-components.svg?)

`樣式（）` 方法適用於我們所有的組件。

```jsx
從'react'中導入React;
導入樣式來自'styled-components';
來自'@ material-ui / core / Button'的導入按鈕;

const StyledButton =樣式（按鈕）`
  背景：線性漸變（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  border-radius：3px;
  邊界：0;
  色：白色;
  身高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135，.3）;
`;

function StyledComponentsButton（）{
  return（
    <div>
      <Button>
        Material-UI
      </Button>
      <StyledButton>
        Styled Components
      </StyledButton>
    </div>
  ）;
}

導出默認StyledComponentsButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/mzwqkk1p7j)

### 控制優先權

樣式組件和JSS都將樣式註入 `<head>`的底部。 確保樣式組件樣式最後加載的一種方法是將CSS注入順序</a>更改為 ，如演示中所示。</p> 

另一種方法是使用 `&` 字在樣式組件至 [顛簸起來特異性](https://www.styled-components.com/docs/advanced#issues-with-specificity) 通過重複類名。 使用此選項可確保在JSS樣式之前應用樣式化組件樣式。 此解決方案的一個示例：

```jsx
從'react'中導入React;
導入樣式來自'styled-components';
來自'@ material-ui / core / Button'的導入按鈕;

const StyledButton =樣式（按鈕）`
  && {
    背景：線性漸變（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
    border-radius：3px;
    邊界：0;
    色：白色;
    高：48px;
    填充：0 30px;
    box-shadow：0 3px 5px 2px rgba（255,105,135，.3）;
  }
`;

函數StyledComponentsButton（）{
  return（
    <div>
      <Button>
        Material-UI
      </Button>
      <StyledButton>
        樣式組件
      </StyledButton>
    </div>
  ）;
}

導出默認StyledComponentsButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/xpp5oj9o0z)

### 更深層的元素

在某些情況下，上述方法不起作用。 例如，如果您嘗試風格 [抽屜](/demos/drawers/) 與變異 `永久的`， ，你可能會需要影響抽屜的底層 `紙` 的風格。

但是，這不是 `抽屜` 的根元素，因此上面的樣式組件自定義將不起作用。 您可以通過使用 [穩定的JSS類名](/customization/css-in-js/#global-css)解決此問題，但最可靠的方法是使用 `類` 屬性來引入覆蓋樣式，然後通過 `&`以更高的特異性對其進行樣式化。

以下示例除了按鈕本身的自定義樣式外，還會覆蓋 `按鈕` 的 `標籤` 樣式。 它還解決了 [這個風格成分問題](https://github.com/styled-components/styled-components/issues/439) 由不應該在底層組件來通過“消耗”的特性。

```jsx
從'react'中導入React;
導入樣式來自'styled-components';
來自'@ material-ui / core / Button'的導入按鈕;

const StyledButton =樣式（（{ color, ...other }）=> （
  <Button {...other} classes={{ label: 'label' }} />
））`
  background：linear-gradient（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  邊界：0;
  色：白色;
  身高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135,0.3）;

  & 標籤{
    顏色：$ {props => props.color};
  }
`;

函數StyledComponentsButton（）{
  return（
    <div>
      <Button>Material-UI</Button>
      <StyledButton color="papayawhip">樣式組件</StyledButton>
    </div>
  ）;
}

導出默認StyledComponentsButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/j4n13yl1r9)

## 情感

Emotion的 **css（）** 方法與Material-UI無縫協作。 **css（）** 返回的類名可以直接傳遞給組件的 `className` prop以覆蓋根樣式。

```jsx
從'react'中導入React;
從'情緒'導入 { css } ;
來自'@ material-ui / core / Button'的導入按鈕;

const buttonStyles = css`
  background：linear-gradient（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  border-radius：3;
  邊界：0;
  色：白色;
  高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135,0.3）;
`;

//我們只是為它們分配Button的className屬性
函數EmotionButton（）{
  return（
    <div>
      <Button>Material-UI</Button>
      <Button className={buttonStyles}>Emotion</Button>
    </div>
  ）;
}

導出默認EmotionButton
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/yw93kl7y0j)

### 更深層的元素

使用 **css（）** 創建的樣式也可以使用 `類` prop映射到類名。 當您想要自定義組件中更深層元素的樣式時，這非常有用。

```jsx
從'react'中導入React;
從'情緒'導入 { css } ;
來自'@ material-ui / core / Button'的導入按鈕;

const的樣式= {
  按鈕：CSS（{
    背景：'線性梯度（45deg，＃fe6b8b 30％，＃ff8e53 90％）'，
    borderRadius：3，
    邊界：0，
    高度：48，
    填充：'0 30px'，
    boxShadow：'0 3px 5px 2px rgba（255,105,135,0.3）'，
  }），
  標籤：css（{
    color: 'papayawhip',
  }），
};

function EmotionButton（）{
  return（
    <div>
      <Button>Material-UI</Button>
      <Button className={styles.button} classes={{ label: styles.label }}>
        Emotion
      </Button>
    </div>
  ）;
}

導出默認EmotionButton
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/4q8o1y975w)

**注意：** 默認情況下，Emotion和JSS都會在 `<head>`的底部注入樣式。 如果您不想使用 **！important**標記樣式屬性，則需要更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如示例中所示。

## 反應情緒

**樣式（）** 函數可用於自定義任何Material-UI組件的根樣式。

```jsx
從'react'中導入React;
進口風格來自'react-emotion';
來自'@ material-ui / core / Button'的導入按鈕;

const StyledButton =樣式（按鈕）`
  背景：線性漸變（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  border-radius：3;
  邊界：0;
  色：白色;
  身高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135,0.3）;
`;

函數ReactEmotionButton（）{
  return（
    <div>
      <Button>Material-UI</Button>
      <StyledButton>React Emotion</StyledButton>
    </div>
  ）;
}

導出默認ReactEmotionButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/xj81yqx504)

**注意：** 默認情況下，Emotion和JSS都會在 `<head>`的底部注入樣式。 如果您不想使用 **！important**標記樣式屬性，則需要更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如示例中所示。

## CSS模塊

![明星](https://img.shields.io/github/stars/css-modules/css-modules.svg?style=social&label=Star)

這是很難知道的市場份額 [這個造型的解決方案](https://github.com/css-modules/css-modules) ，因為它是依賴於 人都在用捆綁的解決方案。

**CssModulesButton.css**

```css
.button {
  background：linear-gradient（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  border-radius：3px;
  邊界：0;
  色：白色;
  高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135，.3）;
}
```

**CssModulesButton.js**

```jsx
從'react'中導入React;
// webpack，parcel或者將CSS注入到'./CssModulesButton.css'的頁面
導入樣式中;
來自'@ material-ui / core / Button'的導入按鈕;

功能CssModulesButton（）{
  return（
    <div>
      <Button>
        Material-UI
      </Button>
      <Button className={styles.button}>
        CSS模塊
      </Button>
    </div>
  ）;
}

導出默認CssModulesButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/m4j01r75wx)

**注意：** JSS在 `<head>`的底部注入其樣式。 如果您不想使用 **！important**標記樣式屬性，則需要更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如演示中所示。

## 全球CSS

明確地為組件提供類名是太費力了嗎？ 請放心，我們提供了一個選項，使類名為 **確定性** 用於快速 原型設計： [`dangerouslyUseGlobalCSS`](/customization/css-in-js/#global-css)。

**GlobalCssButton.css**

```css
.MuiButton-root {
  background：linear-gradient（45deg，＃fe6b8b 30％，＃ff8e53 90％）;
  border-radius：3px;
  邊界：0;
  色：白色;
  高：48px;
  填充：0 30px;
  box-shadow：0 3px 5px 2px rgba（255,105,135，.3）;
}
```

**GlobalCssButton.js**

```jsx
從'react'中導入React;
來自'@ material-ui / core / Button'的導入按鈕;

函數GlobalCssButton（）{
  return（
    <div>
      <Button>
        Global CSS
      </Button>
    </div>
  ）;
}

導出默認GlobalCssButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/2zv5m0j37p)

**注意：** JSS在 `<head>`的底部注入其樣式。 如果您不想使用 **！important**標記樣式屬性，則需要更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如演示中所示。

## 反應JSS

![明星](https://img.shields.io/github/stars/cssinjs/jss.svg?style=social&label=Star) ![NPM](https://img.shields.io/npm/dm/react-jss.svg?)

Material-UI的樣式解決方案與 [react-jss](https://github.com/cssinjs/react-jss)共享許多構建塊。 我們繼續分叉項目以處理我們的獨特需求，但我們正在努力將Material-UI中的更改和修復合併到react-jss。

```jsx
從'react'中導入React;
從'prop-types'導入PropTypes;
從'react-jss / lib / injectSheet'導入injectSheet;
來自'@ material-ui / core / Button'的導入按鈕;

const的樣式= {
  按鈕：{
    背景：'線性梯度（45deg，＃FE6B8B 30％，＃FF8E53 90％）'，
    borderRadius：3，
    邊界：0，
    色：“白色”，
    高度：48，
    填充：'0 30PX'，
    boxShadow：'0 3PX 5px的2px的RGBA（255，105，135，0.3）“，
  }，
};

函數ReactJssButton（props）{
  return（
    <div>
      <Button>Material-UI</Button>
      <Button className={props.classes.button}>react-jss</Button>
    </div>
  ）;
}

ReactJssButton.propTypes = {
  classes：PropTypes.object.isRequired，
};

導出默認的injectSheet（樣式）（ReactJssButton）;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/219x6qqx0p)

## CSS到MUI webpack Loader

用於webpack的 [css-to-mui-loader](https://www.npmjs.com/package/css-to-mui-loader) 允許您編寫可以轉換為JS的CSS，以便與 [`withStyles（）`](/customization/css-in-js/#withstyles-styles-options-higher-order-component) 高階組件一起使用。 它提供了一些用於從CSS中訪問主題的鉤子。

**webpack.config.js**

```js
module.exports = {
  模塊：{
    規則：[
      {
        test：/\.css$/,
        使用：['babel-loader'，'css-to-mui-loader']
      }
    ]
  }
}
```

**CssToMuiButton.css**

```css
.button {
  background： $(theme.palette.primary.main);
  填充：2su; / * Material-UI間距單位* /
}

.button：懸停{
  background： $(theme.palette.primary.light);
}

@media $（theme.breakpoints.down（'sm'））{
  .button {
    font-size： $(theme.typography.caption.fontSize);
  }
}
```

**CssToMuiButton.js**

```js
從'@ material-ui / core / Button'導入按鈕;
從'@ material-ui / core / styles'導入 { withStyles } ;來自'./CssToMuiButton.css'的
導入樣式;

const CssToMuiButton = withStyles（styles）（（{ classes }）=> （
  <Button className={classes.button}>
    CSS to MUI Button
  </Button>
））;
```

## 魅力

![明星](https://img.shields.io/github/stars/threepointone/glamor.svg?style=social&label=Star) ![NPM](https://img.shields.io/npm/dm/glamor.svg?)

使用Glamour應用樣式的好方法是使用 **css（）** 函數，然後使用 **類名** 將它們作為字符串：

```jsx
從'react'中導入React;
從'迷人'進口迷人;
來自'魅力'的 { css } 進口;從'classnames'導入
類名;
來自'@ material-ui / core / Button'的導入按鈕;

常量buttonStyles = {
  背景：'線性梯度（45deg，＃FE6B8B 30％，＃FF8E53 90％）'，
  borderRadius：3，
  邊界：0，
  顏色：“白色”，
  高度：48，
  填充：'0 30px'，
  boxShadow：'0 3px 5px 2px rgba（255,105,135，.3）'，
};

//首先我們得到帶有Glamour css函數
const buttonClasses = css（buttonStyles）的classNames;

//我們需要將類名稱作為字符串
const className = buttonClasses.toString（）;

//然後我們只為它們分配Button的className屬性
function GlamourButton（）{
  return（
    <div>
      <Button>
        Material-UI
      </Button>
      <Button className={className}>
        Glamour
      </Button>
    </div>
  ）;
}

導出默認GlamourButton;
```

[![編輯按鈕](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/ov5l1j2j8z)

**注意：** Glamour和JSS都在 `<head>`的底部注入了他們的風格。 如果您不想使用 **！important**標記樣式屬性，則需要更改 [CSS注入順序](/customization/css-in-js/#css-injection-order)，如演示中所示。