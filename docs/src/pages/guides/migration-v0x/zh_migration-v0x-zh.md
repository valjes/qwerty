# 從v0.x遷移

<p class="description">是的，v1已經發布了！ 利用2年的努力。</p>

## 常問問題

### 哇 - API有所不同！ 這是否意味著1.0完全不同，我將不得不重新學習基礎知識，遷移幾乎是不可能的？

我很高興你問！ 答案是不。核心概念沒有改變。 您會注意到API提供了更大的靈活性，但這需要付出代價。 我們一直在製作較低級別的組件，從而減少了複雜性。

### 是什麼推動了這麼大的變化？

材料的UI開始 [3年前](https://github.com/mui-org/material-ui/commit/28b768913b75752ecf9b6bb32766e27c241dbc46)。 從那時起，生態系統發展了很多，我們也學到了很多東西。 [@nathanmarks](https://github.com/nathanmarks/) 開始了一項雄心勃勃的任務，從 **基礎** 重建Material-UI，利用這些知識來解決長期存在的問題。 列舉一些主要變化：

- 使用CSS-在-JS新造型液（最好 [定制](/customization/overrides/) 功耗，性能越好）
- 新 [主題處理](/customization/themes/) （嵌套，自支撐等）
- 感謝 [Next.js](https://github.com/zeit/next.js)快速創建文檔
- 方式更好 [測試覆蓋率](/guides/testing/) （99％以上，在所有主流瀏覽器上運行， [視覺回歸測試](https://www.argos-ci.com/mui-org/material-ui)）
- 完全 [服務器端渲染](/guides/server-rendering/) 支持
- 廣泛的 [支持的瀏覽器](/getting-started/supported-platforms/)

### 我應該從哪裡開始遷移？

1. 首先在v0.x版本旁邊安裝v1.x版本的Material-UI。
    
    用紗線：
    
    ```sh
    紗線添加材料-ui
    紗線添加@ material-ui / core
    ```
    
    或者使用npm：
    
    ```sh
    npm install material-ui
    npm install @ material-ui / core
    ```
    
    然後
    
    ```js
    從'material-ui / FlatButton'導入FlatButton; // v0.x
    導入來自'@ material-ui / core / Button'的按鈕; // v1.x
    ```

2. 在項目上運行 [遷移幫助程序](https://github.com/mui-org/material-ui/tree/master/packages/material-ui-codemod)。

3. `MuiThemeProvider` 對於v1.x.是可選的，但如果您有自定義主題，則可以同時使用該組件的v0.x和v1.x版本，如下所示：
    
    ```jsx
    從'react'中導入React;
    從'@ material-ui / core / styles'導入 { MuiThemeProvider, createMuiTheme } ; // v1.x
    從'material-ui'導入 { MuiThemeProvider as V0MuiThemeProvider} ;
    從'material-ui / styles / getMuiTheme'導入getMuiTheme;
    
    const theme = createMuiTheme（{
    / *主題為v1.x * /
    }）;
    const themeV0 = getMuiTheme（{
    / *主題為v0.x * /
    }）;
    
    function App（）{
    return（
      <MuiThemeProvider theme={theme}>
        <V0MuiThemeProvider muiTheme={themeV0}>
          {/ * Components * /}
        </V0MuiThemeProvider>
      </MuiThemeProvider>
    ）;
    }
    
    export default App;
    ```

4. 之後，您可以隨時遷移一個組件實例。

## 組件

### 自動完成

Material-UI不提供用於解決此問題的高級API。 你鼓勵你去探索 [的解決方案做出反應的社區已建成](/demos/autocomplete/)。

將來，我們將研究提供一個簡單的組件來解決簡單的用例： [＃9997](https://github.com/mui-org/material-ui/issues/9997)。

### Svg圖標

在項目上運行 [遷移幫助程序](https://github.com/mui-org/material-ui/tree/master/packages/material-ui-codemod)。

這將應用如下更改：

```diff
- 從'material-ui / svg-icons / Add'導入AddIcon;
+從'@ material-ui / icons / Add'導入AddIcon;

<AddIcon />
```

### 平面按鈕

```diff
-inmport FlatButton來自'material-ui / FlatButton';來自'@ material-ui / core / Button'的
+導入按鈕;

-<FlatButton />
+<Button />
```

### 凸起的按鈕

```diff
-import來自'material-ui / RaisedButton'的RaisedButton;來自'@ material-ui / core / Button'的
+導入按鈕;

-<RaisedButton />
+<Button variant="contained" />
```

### 副標題

```diff
-import來自'material-ui / Subheader'的副標題;
+從'@ material-ui / core / ListSubheader'導入ListSubheader;

-<Subheader>副標題</Subheader>
+<ListSubheader>副標題</ListSubheader>
```

### 切換

```diff
-import從'material-ui / Toggle'切換;
+ import從'@ material-ui / core / Switch'切換;

-<Toggle

-  toggled={this.state.checkedA}
-  onToggle={this.handleToggle}
-/>
+<Switch
+  checked={this.state.checkedA}
+  onChange={this.handleSwitch}
+/>
```

### 菜單項

```diff
-import來自'material-ui / MenuItem'的MenuItem;
+從'@ material-ui / core / MenuItem'導入MenuItem;

-<MenuItem primaryText="Profile" />
+<MenuItem>簡介</MenuItem>
```

### 字體圖標

```diff
-import來自'material-ui / FontIcon'的FontIcon;
+從'@ material-ui / core / Icon'導入圖標;

-<FontIcon>家</FontIcon>
+<Icon>家</Icon>
```

### 循環進展

```diff
-import來自'material-ui / CircularProgress'的CircularProgress;
+從'@ material-ui / core / CircularProgress'導入CircularProgress;

-<CircularProgress mode="indeterminate" />
+<CircularProgress variant="indeterminate" />
```

### 下拉式菜單

```diff
-import DropDownMenu來自'material-ui / DropDownMenu';
+ import從'@ material-ui / core / Select'中選擇;

-<DropDownMenu></DropDownMenu>
+<Select value={this.state.value}></Select>
```

### 未完待續…

您是否已成功遷移您的應用，並希望幫助社區？ 請幫助我們！ 我們有一個未解決的問題，以完成此遷移指南 [＃7195](https://github.com/mui-org/material-ui/issues/7195)。 歡迎任何拉動請求