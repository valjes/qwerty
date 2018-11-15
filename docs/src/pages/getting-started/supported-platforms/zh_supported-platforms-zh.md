# 支持的平台

<p class="description">了解Material-UI支持的從現代到舊的平台。</p>

## 瀏覽器

Material-UI支持所有主流瀏覽器和平台的最新穩定版本。 我們還支持Internet Explorer 11。 您不需要提供任何JavaScript polyfill，因為我們在內部和單獨管理不受支持的瀏覽器功能。

| IE | 邊緣     | 火狐     | 鉻      | 蘋果瀏覽器  | Googlebot的 |
|:-- |:------ |:------ |:------ |:------ |:---------- |
| 11 | > = 14 | > = 52 | > = 49 | > = 10 | ✅          |

由於Googlebot使用Web呈現服務（WRS）來索引頁面內容，因此Material-UI支持它至關重要。 [WRS基於Chrome 41](https://developers.google.com/search/docs/guides/rendering)。 您可以期望Material-UI的組件在沒有重大問題的情況下呈現。

## 服務器

因為Material-UI支持服務器端渲染，所以我們需要支持 [Node.js](https://github.com/nodejs/node)的最新穩定版本。 我們試圖支持 [最後一個活動LTS版本](https://github.com/nodejs/Release#lts-schedule1)。 現在，我們支持 **節點v6.x** 和更新版本。