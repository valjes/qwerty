---
title: Transition React組件
components: 折疊，淡入淡出，成長，滑動，縮放
---
# 轉變

<p class="description">過渡有助於使UI富有表現力且易於使用。</p>

Material-UI提供了許多轉換，可用於向應用程序組件引入一些基本的 [motion](https://material.io/design/motion/) 。

為了更好地支持服務器渲染，Material-UI為某些過渡組件（淡入淡出，增長，縮放，幻燈片）的子項提供了 `樣式` 屬性 。 必須將 `style` 屬性應用於DOM才能使動畫按預期工作。

```jsx
//`props`對象包含`style`屬性。
//你需要將它提供給`div`元素，如下所示。
function MyComponent（props）{
  return（
    <div {...props}>
      Fade
    </div>
  ）;
}

export default Main（）{
  return（
    <Fade>
      <MyComponent />
    </Fade>
  ）;
}
```

## 坍方

從子元素的頂部垂直展開。 `collapsedHeight` 屬性可用於設置未展開時的最小高度。

{{“demo”：“pages / utils / transitions / SimpleCollapse.js”}}

## 褪色

從透明淡入淡出到不透明。

{{“demo”：“pages / utils / transitions / SimpleFade.js”}}

## 增長

從子元素的中心向外擴展，同時從 透明變為不透明。

第二個示例演示如何更改 `transform-origin`，並有條件地應用 `timeout` 屬性來更改輸入速度。

{{“demo”：“pages / utils / transitions / SimpleGrow.js”}}

## 滑動

從屏幕邊緣滑入。 `方向` 屬性控制轉換從哪個邊緣開始。

Transition組件的 `mountOnEnter` 屬性可防止子組件安裝 直到 `中的` 為 `真`。 這可以防止相對定位的組件從其屏幕外位置滾動到視圖 。 類似地， `unmountOnExit` 屬性在從屏幕轉換後從DOM中刪除組件 。

{{“demo”：“pages / utils / transitions / SimpleSlide.js”}}

## 放大

從子元素的中心向外擴展。

此示例還演示瞭如何延遲輸入轉換。

{{“demo”：“pages / utils / transitions / SimpleZoom.js”}}