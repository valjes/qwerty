# 與其他圖書館比較

<p class="description">您在這裡是因為您想知道Material-UI是否可以更好地解決您的具體問題。 這就是我們希望在這里為您解答的問題。</p>

這絕對是編寫指南中最具挑戰性的頁面之一，但我們確實認為這很重要。 可能的情況是，你遇到了你試圖解決的問題，並且你已經使用了另一個庫來解決它們。

我們希望您幫助保持此文檔的最新狀態，因為JavaScript世界快速發展！ 如果您發現不准確或者看起來不太正確的事情，請通過 [告知我們問題](https://github.com/mui-org/material-ui/issues/new?title=[docs]+Inaccuracy+in+comparison+guide)。

我們涵蓋以下圖書館：

- [材料的UI](#material-ui)
- [Material Design Lite（MDL）](#material-design-lite-mdl-)
- [材料組件Web（MDC-web）](#material-components-web-mdc-web-)
- [物質化](#materialize)
- [反應工具箱](#react-toolbox)

## 材料的UI

![明星](https://img.shields.io/github/stars/mui-org/material-ui.svg?style=social&label=Stars) ![npm下載](https://img.shields.io/npm/dm/@material-ui/core.svg)

我們會盡力避免偏見，雖然作為核心團隊，我們顯然很喜歡Material-UI❤️。 我們認為它解決的問題比其他任何問題都要好;如果我們不相信，我們就不會這樣做😄。

我們確實希望公平和準確，所以在其他圖書館提供顯著優勢的地方，我們也嘗試列出這些。

## Material Design Lite（MDL）

![明星](https://img.shields.io/github/stars/google/material-design-lite.svg?style=social&label=Stars) ![npm下載](https://img.shields.io/npm/dm/material-design-lite.svg)

Material Design Lite雖然是一個經過深思熟慮的Material Design實現，但 主要由Google的Developer Relations維護。 今天， **該項目不再維護**。 所以發生了什麼事？

材料組件Web團隊已經開始建造MDC-Web作為“MDL V2”，但是，它合作了幾個月後， 兩隊覺得最好帶上材質設計團隊的職權範圍內的項目。 這種轉變意味著重新定位目標，而不是簡單地將“材料設計外觀和感覺”添加到網站， 以及實現整個網絡平台的規範材料設計實現的目標。

## 材料組件Web（MDC-web）

![明星](https://img.shields.io/github/stars/material-components/material-components-web.svg?style=social&label=Stars) ![npm下載](https://img.shields.io/npm/dm/material-components-web.svg)

我們很高興看到Google及其設計團隊支持該項目。 它發出了一個明確的信號，即 [材料設計規範](https://material.io/design/) 在這裡保持 ，因為他們繼續投資它。

### 框架和庫

材料UI只關注圖書館做出反應，雖然，因為Preact支持非常相同的API， 我們希望能盡快支持這一點。 支持一個框架可以讓我們做得更少，但做得更好。

這有不同的風格：

- 由於約束較少，我們可以根據目標框架進行權衡。 我們需要考慮更少的邊緣情況。
- 我們可以花更多的時間來確定React用例。

MDC-web從一開始就設計為與第三方JS框架和庫完全兼容。 他們在github [README](https://github.com/material-components/material-components-web/#material-components-for-the-web)列出了第三方框架集成項目

### 造型解決方案

[Material-UI帶有風格](https://github.com/oliviertassinari/a-journey-toward-better-style)的重要遺產。 我們的第一個版本是使用較少，但看到這種解決方案的限制， 我們很快開始尋找到替代品。 我們的第一次遷移是使用內聯式解決方案。 這很有希望：

- 它允許我們為用戶刪除對LESS工具鏈的依賴。 我們在安裝過程中刪除了一個重要的摩擦。 （**更簡單**）
- 我們能夠在運行時更改主題，嵌套不同的主題，並具有動態樣式。 （**更強大**）
- 我們通過打破大的單片CSS文件來減少加載時間，以便啟用代碼分割。 （**更快**）
- 樣式覆蓋故事變得更直觀，因為我們沒有CSS特異性問題。 （**更簡單**）

最終，我們達到了內聯樣式的局限性，並轉向了CSS-in-JS 解決方案。 這種轉變是在不失去第一次遷移引入的增強的情況下完成的。 **我們強烈認為CSS-in-JS是Web平台的未來**。 你可以 [了解更多關於我們的新造型的解決方案](/customization/css-in-js/) 的文件中。

MDC-web依賴於SCSS作為Bootstrap v4。 SCSS架構與LESS- 非常接近，這是我們為其局限性而取代的技術。

### 願景

我們的願景是提供材料設計指南 **和更多的優雅實施**。

> 材料設計指南是一個令人難以置信的起點，但它們並未提供有關應用程序所有方面或需求的指導。 除了特定於指南的實現之外，我們還希望Material-UI成為應用程序開發通常有用的任何內容，所有這些都符合Material Design準則的精神。
> 
> *[摘自文獻的 [視覺部分](/discover-more/vision/)]*

我們希望看到企業採取材料-UI的優勢，出貨的真棒UI給他們的用戶成功 ，而有它自己的品牌相匹配，所以我們在材質的UI定制功能投入了很多。

MDC-Web的唯一目標是成為Web平台的Material Design實現。 **沒有更多，沒有更少**。 他們不會考慮對組件進行更改 - 尤其是用戶體驗更改 - 這會以犧牲核心Material Design系統為代價來促進額外的靈活性，因為這是項目的非目標。 *[來源](https://github.com/mui-org/material-ui/issues/6799#issuecomment-299925174)*

### 測試

這兩個項目都在測試中投入了很多。 在撰寫本文時，兩個項目的測試覆蓋率均超過99％：

- Material-UI在Chrome 49，Firefox 45，Safari 10和Edge 14上運行了1200多個單元測試。
- MDC-web在所有主流瀏覽器上運行1200多個單元測試。

儘管如此，還是有一件事讓Material-UI脫穎而出，這是關鍵： 當MDC-web沒有任何時候，我們有 [百個視覺回歸測試](https://www.argos-ci.com/mui-org/material-ui)。 通過視覺回歸測試，您無需進行任何權衡：

- 您可以花更少的時間確保每個貢獻都不會引入意外的回歸。 在 **小於** 時，你在一個單一的貢獻花，在 **以上** 捐款可以接受。
- 你可以合併新的貢獻，而不需要挖掘太多。 實際上，您不是在等待用戶報告回歸。 它是 **有效** 和 **提高了圖書館質量**。

## 物質化

![明星](https://img.shields.io/github/stars/Dogfalo/materialize.svg?style=social&label=Stars) ![npm下載](https://img.shields.io/npm/dm/materialize-css.svg)

### 瀏覽器支持

Materialize支持比Material-UI更廣泛的瀏覽器，例如， 支持IE 10，而 [支持IE 11](/getting-started/supported-platforms/)。 只支持IE 11，我們才能充分利用flexbox佈局。 IE 10與flexbox有很多問題。

### 造型解決方案

Materialise使用SCSS，一種造型架構Material-UI從2年前開始移動。 我們在上面的 [MDC-web部分](#styling-solution) 解釋了原因。

## 反應工具箱

![明星](https://img.shields.io/github/stars/react-toolbox/react-toolbox.svg?style=social&label=Stars) ![npm下載](https://img.shields.io/npm/dm/react-toolbox.svg)

### 造型解決方案

雖然React Toolbox和Material-UI都在關注CSS-in-JS，但我們採取了不同的權衡。 Material-UI選擇了 **JSS** 而React Toolbox開始用 **樣式組件重寫他們的庫**。 我們在樣式組件上選擇了JSS，原因如下：

- JSS公開了一個低級API： 
  - 我們可以根據我們的獨特需求進行建模，這使我們能夠構建最先進的覆蓋和主題機制之一。
  - 它沒有像 `樣式的組件` 那樣耦合到React。 它有可能覆蓋任何第三方JS框架和庫。 可以使用SCSS進行相似之處。 SCSS與任何JavaScript框架和庫兼容，有助於它在社區中獲得牽引力。
- JSS是 [快兩倍](https://github.com/A-gambit/CSS-IN-JS-Benchmarks/blob/master/RESULT.md) 安裝組件比風格的成分是，所有的優化開啟。

這並不是說Material-UI是關於用戶如何編寫樣式的觀點。 如果您願意，可以使用樣式組件。