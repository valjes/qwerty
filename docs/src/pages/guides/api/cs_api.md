# API設計方法

<p class="description">我們已經學習了很多關於如何使用Material-UI的知識，而v1重寫允許我們完全重新思考組件API。</p>

> API設計很難，因為你可以讓它看起來很簡單，但它實際上看似複雜，或者說它實際上很簡單但看起來很複雜。

[@sebmarkbage](https://twitter.com/sebmarkbage/status/728433349337841665)

塞巴斯蒂安Markbage [指出，](https://2014.jsconf.eu/speakers/sebastian-markbage-minimal-api-surface-area-learning-patterns-instead-of-frameworks.html)，沒有抽象優於錯誤的抽象。 我們提供低級組件以最大化組合功能。

## 組成

您可能已經註意到API中有關組合組件的一些不一致之處。 為了提供一些透明度，我們在設計API時一直使用以下規則：

1. 使用 `children` 屬性是使用React進行合成的慣用方法。
2. 有時我們只需要有限的子組成，例如當我們不需要允許子順序排列時。 在這種情況下，提供顯式屬性可以使實現更簡單，更高效;例如， `Tab` 採用 `圖標` 和 `標籤` 屬性。
3. API一致性很重要。

## 規則

除了上述構成權衡之外，我們還執行以下規則：

### 傳播

提供的未記錄的屬性傳播到根元素;例如， 將 `className` 屬性應用於根。

現在，假設你要禁用 `MenuItem`上的漣漪。 您可以利用傳播行為：

```jsx
<MenuItem disableRipple />
```

`disableRipple` 屬性將以這種方式流動： [`MenuItem`](/api/menu-item/) > [`ListItem`](/api/list-item/) > [`ButtonBase`](/api/button-base/)。

### 原生屬性

我們避免記錄DOM支持的本機屬性，如 [`className`](/customization/overrides/#overriding-with-class-names)。

### CSS類

所有組件都接受 [`class`](/customization/overrides/#overriding-with-classes) 屬性來自定義樣式。 類設計回答了兩個約束： 使類結構盡可能簡單，同時足以實現Material Design規範。

- 應用於根元素的類始終稱為 `root`。
- 所有默認樣式都分組在一個類中。
- 應用於非根元素的類以元素的名稱為前綴，例如Dialog組件中的 `paperWidthXs`。
- 由布爾屬性 **應用的變體不是** 前綴，例如由 `舍入` 屬性應用的 `舍入` 類 。
- 由枚舉屬性 **應用的變體是** 前綴的，例如由 `color =“primary”` 屬性應用的 `colorPrimary` class 。
- 變體具有 **個特異性水平**。 `色` 和 `變體` 屬性被認為是變體。 樣式特性越低，覆蓋越簡單。
- 我們增加變體修飾符的特異性。 我們已經 **必須這樣做** 為偽類（`：懸停`， `：聚焦`等）。 它允許更多的控制，但代價是更多的樣板。 希望它也更直觀。

```js
常量樣式= {
  根：{
    顏色：綠[600]，
    '&$checked'：{
      顏色：綠[500]，
    }，
  }，
  檢查：{}，
};
```

### 嵌套組件

組件內的嵌套組件具有：

- 當它們是頂級組件抽象的關鍵時，它們自己的扁平屬性，例如 和 `輸入` 組件的 `id` 屬性。
- 當用戶可能需要調整內部渲染方法的子組件時，他們自己的 `xxxProps` 屬性，例如 ，在內部使用 `輸入` 組件上公開 `inputProps` 和 `InputProps` 屬性。
- 他們自己的 `xxxComponent` 屬性，用於執行組件注入。
- 當用戶可能需要執行命令性操作時，他們自己的 `xxxRef` 屬性，例如 ，暴露 `inputRef` 屬性以訪問 `Input` 組件上的本機 `輸入`。 這有助於回答問題 [“如何訪問DOM元素？”](/getting-started/faq/#how-can-i-access-the-dom-element-)

### 物業命名

應根據 **默認值**選擇布爾屬性的名稱。 例如，輸入元素上的 `disabled` 屬性（如果提供）默認為 `true`。 這個選擇允許簡寫符號：

```diff
-<Input enabled={false} />
+<Input disabled />
```

### 受控組件

大多數受控部件的經由控制 `值` 和 `的onChange` 性能， 然而， `開放` / `的OnClose` / `的OnOpen` 組合用於顯示相關的狀態。

### boolean vs enum

為組件的變體設計API有兩種選擇：使用 *布爾值*;或者 *枚枚數*。 例如，讓我們選擇具有不同類型的按鈕。 每個選項都有其優點和缺點：

- 選項1 *布爾值*：
    
    ```tsx
    類型Props = {
    contains：boolean;
    fab：boolean;
    };
    ```
    
    此API使能簡化符號： `<Button>`， `<Button contained />`， `<Button fab />`。

- 選項2 *枚舉*：
    
    ```tsx
    類型Props = {
    variant：'text'| '包含'| “FAB”;
    }
    ```
    
    此API是更詳細的： `<Button>`， `<Button variant="contained">`， `<Button variant="fab">`。
    
    但是，它可以防止使用無效組合， 限制公開的屬性數量， 並且可以在將來輕鬆支持新值。

Material-UI組件根據以下規則使用兩種方法的組合：

- 當需要 **2** 自由度時，使用 *布爾值*。
- 當需要 **> 2** 個自由度時，或者如果將來可能需要額外的自由度，則使用 *枚舉*。

回到上一個按鈕示例;因為它需要3個自由度，我們使用 *枚舉*。