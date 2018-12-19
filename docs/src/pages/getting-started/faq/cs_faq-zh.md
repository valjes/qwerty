# 經常問的問題

<p class="description">堅持一個特定的問題？ 首先檢查一些常見問題。</p>

如果你仍然無法找到你想要的東西，你可以向社區詢問 [gitter](https://gitter.im/mui-org/material-ui)。 對於操作方法問題和其他非問題，請使用 [StackOverflow](https://stackoverflow.com/questions/tagged/material-ui) 而不是Github問題。 有一個名為 `material-ui` 的StackOverflow標記，可用於標記您的問題。

## 為什麼我的組件在生產版本中沒有正確呈現？

一旦您的代碼在生產捆綁包中，這可能是由於類名衝突而發生的n°1問題。 要使Material-UI起作用，頁面上所有組件的 `classNames` 值必須由 [類名生成器](/customization/css-in-js/#creategenerateclassname-options-class-name-generator)的單個實例生成。

要糾正此問題，需要初始化頁面上的所有組件，以便它們之間只有 **個類名生成器**。

您最終可能會在各種情況下意外使用兩個類名生成器：

- 你一不小心 **束** 兩個版本材質的UI。 您可能有一個依賴項沒有正確設置Material-UI作為對等依賴項。
- 您正在使用 `JssProvider` 作為React Tree的 **個子集**。
- 您正在使用捆綁器，它以某種方式拆分代碼，從而導致創建多個類名生成器實例。 >如果您使用帶有 [SplitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/)的webpack，請嘗試在 `優化`</a>下配置 `runtimeChunk` 設置。</li> </ul> 
    
    總的來說，通過將每個Material-UI應用程序包含在其組件樹 **頂部的 [`JssProvider`](/customization/css-in-js/#jssprovider) 組件並使用它們之間共享的單個類名生成器**，可以很容易地從此問題中恢復。
    
    [分辨率示例](/customization/css-in-js/#jssprovider)。 任何解決方案的最後一部分將根據您使用的Bundler而有所不同，但總體目標是確保包含上述第一個代碼段的公共模塊僅加載並運行一次。
    
    ⚠️你趕時間嗎？ 請放心，我們提供了一個選項，使類名為 **deterministic** 作為快速逃生艙： [`dangerouslyUseGlobalCSS`](/customization/css-in-js/#global-css)。
    
    ## 為什麼固定定位元素在打開模態時會移動？
    
    一旦打開模態，我們就會阻止滾動。 當模態應該是唯一的交互式內容時，這可以防止與背景交互，但是，刪除滾動條可以使 **固定定位元素** 移動。 在這種情況下，您可以應用全局 `.mui-fixed` 類名稱來告訴Material-UI處理這些元素。
    
    ## 如何在整個應用中禁用漣漪效應？
    
    目前最好的解決方案是為所有顯示紋波的Material-UI組件編寫包裝組件。 漣漪效應完全來自 `BaseButton` 組件。 您可以在此處使用ButtonBase [找到組件](https://github.com/mui-org/material-ui/search?utf8=%E2%9C%93&q=%22%2F%2F+%40inheritedComponent+ButtonBase%22)。 然後，您所要做的就是提供 `disableRipple` 屬性。
    
    ## 我是否必須使用JSS來設計我的應用程序？
    
    強烈推薦：
    
    - 它內置，因此不會產生額外的捆綁大小開銷。
    - 它速度快 & 內存使用效率。
    - 它有一個乾淨，一致的 [API](http://cssinjs.org/json-api/)。
    - 它支持許多高級功能，無論是本機還是通過 [插件](http://cssinjs.org/plugins/)。
    
    但是，您可能正在為已經使用其他樣式解決方案的應用添加一些Material-UI組件，或者已經熟悉不同的API，並且不想學習新的？ 在這種情況下，請轉到 [樣式庫互操作性](/guides/interoperability/) 部分，其中我們展示了使用替代樣式庫重新設置Material-UI組件是多麼簡單。
    
    ## 我什麼時候應該使用內聯式vs類？
    
    根據經驗，僅對動態樣式屬性使用內聯樣式。 CSS替代方案提供了更多優勢，例如：
    
    - 自動前綴
    - 更好的調試
    - 媒體查詢
    - 關鍵幀
    
    ## 我如何使用react-router？
    
    我們已經記錄瞭如何使用帶有 `ButtonBase` 組件的 [第三方路由庫](/demos/buttons/#third-party-routing-library)。 我們的許多交互式組件的在內部使用： `按鈕`， `菜單項`， `<ListItem button />`， `標籤`等 您可以使用相同的解決方案。
    
    ## 如何將 `withStyles（）` 和 `Theme（）` ` HOC組合？</h2>

<p>有許多不同的選擇：</p>

<p><strong><code>withTheme` 選項：</strong></p> 
    
    ```js
    export default withStyles（styles， { withTheme: true }）（Modal）;
    ```
    
    **`compose（）` 輔助函數：**
    
    ```js
    從'recompose'導入 { compose } ;
    
    導出默認撰寫（
      withTheme（），
      withStyles（styles）
    ）（模態）;
    ```
    
    **原始功能鏈：**
    
    ```js
    導出默認withTheme（）（withStyles（樣式）（模態））;
    ```
    
    ## 如何訪問DOM元素？
    
    使用 [`RootRef`](/api/root-ref/) 幫助程序包裝組件。
    
    ## 為什麼我看到的顏色與我在這裡看到的顏色不同？
    
    文檔站點使用自定義主題。 因此，調色板與Material-UI發布的默認主題不同。 請參閱本頁</a> 了解主題定制。</p> 
    
    ## Material-UI很棒。 我該如何支持該項目？
    
    有很多方法可以支持Material-UI：
    
    - 提高 [的文檔](https://github.com/mui-org/material-ui/tree/master/docs)。
    - 幫助他人入門。
    - [傳播單詞](https://twitter.com/MaterialUI)。
    - 回答 [StackOverflow對存儲庫中標記為問題](https://stackoverflow.com/questions/tagged/material-ui) </a> 或 問題提出疑問。</li> </ul> 
        
        如果您在商業項目中使用Material-UI並希望通過成為 **贊助商**或側面或業餘愛好項目來支持其持續開發，並希望成為支持者，您可以通過 [OpenCollective](https://opencollective.com/material-ui)。
        
        募集的所有資金都是透明管理的，贊助商可以在README和Material-UI主頁上獲得認可。