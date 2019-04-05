# 組成

<p class="description">Material-UI嘗試使合成盡可能簡單。</p>

## 包裝組件

為了提供最大的靈活性和性能， 我們需要一種方法來知道組件接收子元素的性質。 為了解決這個問題，我們在需要 時使用 `muiName` 靜態屬性標記我們的一些組件。

但是，用戶喜歡包裝組件以增強它們。 這可能與我們的 `muiName` 解決方案相衝突。 如果遇到此問題，則需要：

1. 轉發屬性。
2. 對包裝組件使用的包裝組件使用相同的標記。

我們來看一個例子：

```jsx
const WrappedIcon = props => <Icon {...props} />;
WrappedIcon.muiName ='Icon';
```

{{“demo”：“pages / guides / composition / Composition.js”}}

## 組件屬性

Material-UI允許您更改將通過名為 `component`的屬性呈現的根節點。 該組件將呈現如下：

```js
return React.createElement（this.props.component，props）
```

例如，默認情況下， `List` 將呈現 `<ul>` 元素。 這可以通過將 [React組件](https://reactjs.org/docs/components-and-props.html#functional-and-class-components) 傳遞給 `組件` 屬性來更改。 以下示例將使用 `<nav>` 元素作為根節點呈現 `List` 組件：

```jsx
<List component="nav">
  <ListItem>
    <ListItemText primary="Trash" />
  </ListItem>
  <ListItem>
    <ListItemText primary="Spam" />
  </ListItem>
</List>
```

這種模式非常強大，可以提供很大的靈活性，以及​​與其他庫（例如 `react-router` 或您喜歡的表單庫）進行互操作的方法。 但是，這也 **帶有一個小的警告！**

### 注意與內聯

使用內聯函數作為 `組件` 屬性的參數可能會導致 **意外的卸載**，因為每次React呈現時都會將新組件傳遞給 `組件` 屬性。 例如，如果要創建充當鏈接的自定義 `ListItem` ，則可以執行以下操作：

```jsx
const ListItemLink =（{icon，primary，secondary，to}）=> （
  <li>
    <ListItem button component={props => <Link to={to} {...props} />}>
      {icon && <ListItemIcon>{icon}</ListItemIcon>}
      <ListItemText inset primary={primary} secondary={secondary} />
    </ListItem>
  </li>
）;
```

但是，由於我們使用內聯函數來更改呈現的組件，因此React將在每次呈現 `ListItemLink` 時卸載鏈接。 不僅React不必要地更新DOM， `ListItem` 的連鎖效果也將無法正常工作。

解決方案很簡單： **避免內聯函數，並將靜態組件傳遞給 `組件` 屬性**。 讓我們將 `ListItemLink` 更改為以下內容：

```jsx
class ListItemLink擴展了React.Component {
  renderLink = itemProps => <Link to={this.props.to} {...itemProps} />;

  render（）{
    const {icon，primary，secondary，to} = this.props;
    返回（
      <li>
        <ListItem button component={this.renderLink}>
          {icon && <ListItemIcon>{icon}</ListItemIcon>}
          <ListItemText inset primary={primary} secondary={secondary} />
        </ListItem>
      </li>
    ）;
  }
}
```

`renderLink` 現在將始終引用相同的組件。

### 反應路由器

這是一個帶有 [React Router](https://github.com/ReactTraining/react-router)的演示：

{{“demo”：“pages / guides / composition / ComponentProperty.js”}}