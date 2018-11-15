# 基本

<p class="description">Material Design佈局通過使用統一的元素和間距來鼓勵跨平台，環境和屏幕大小的一致性。</p>

## 響應式用戶界面

[Material Design中的響應式佈局](https://material.io/design/layout/responsive-layout-grid.html) 適應任何可能的屏幕尺寸。 我們提供以下幫助程序以使UI響應：

- [網格](/layout/grid/)：網格在佈局之間創建視覺一致性，同時允許各種設計的靈活性。

- [隱藏](/layout/hidden/)：隱藏組件可用於更改元素的可見性。

- [斷點](/layout/breakpoints/)：我們提供了一個低級API，用於在各種各樣的上下文中使用斷點。

## z-index的

一些Material-UI組件使用 `z-index`，CSS屬性通過提供第三個軸來排列內容來幫助控制佈局。 我們在Material-UI中使用默認的z-index比例，該比例被設計為正確分層抽屜，模態，零食欄，工具提示等。

[這些值](https://github.com/mui-org/material-ui/blob/master/packages/material-ui/src/styles/zIndex.js) 從任意數字開始，高且具體到足以理想地避免衝突。

- 移動步進：1000
- app bar：1100
- 抽屜：1200
- 模態：1300
- snackbar：1400
- 工具提示：1500

始終可以自定義這些值。 您將在 [`zIndex`](/customization/default-theme/?expend-path=$.zIndex) 鍵下的主題中找到它們。 我們不鼓勵定制個人價值觀;如果你換一個，你可能需要改變它們。