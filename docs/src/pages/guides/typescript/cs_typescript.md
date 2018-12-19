# 打字稿

<p class="description">您可以向JavaScript添加靜態類型，以通過TypeScript提高開發人員的工作效率和代碼質量。</p>

看一下使用TypeScript</a> 示例的 Create React App。 需要最低版本的TypeScript 2.8。</p> 

我們的定義使用以下 [tsconfig.json](https://github.com/mui-org/material-ui/tree/master/tsconfig.json)進行測試。 使用不太嚴格的 `tsconfig.json` 或省略某些庫可能會導致錯誤。

## 使用 `withStyles`

在TypeScript中使用 `withStyles` 可能有點棘手，但有一些實用程序可以使體驗盡可能輕鬆。

### 使用 `createStyles` 來打敗類型擴展

常見的混淆源是TypeScript的 [類型擴展](https://blog.mariusschulz.com/2017/02/04/typescript-2-1-literal-type-widening)，這導致此示例無法按預期工作：

```ts
const styles = {
  root： {
    display: 'flex',
    flexDirection: 'column',
  }
};

withStyles（樣式）;
// ^^^^^^
//屬性'flexDirection'的類型不兼容。
//類型'string'不能賦值為'“ -  moz-initial”| “繼承”| “初始”| “還原”| “未設置”| “專欄”| “column-reverse”| “行”...'。
```

問題是 `flexDirection` 屬性的類型被推斷為 `字符串`，這太任意了。 要解決此問題，您可以將樣式對象直接傳遞給 `withStyles`：

```ts
withStyles（{
  根： {
    display: 'flex',
    flexDirection: 'column',
  }，
}）;
```

然而，如果您嘗試使樣式取決於主題，則類型擴展會再次顯示其醜陋的頭部：

```ts
withStyles（（{ palette, spacing }）=> （{
  root：{
    display：'flex'，
    flexDirection：'column'，
    padding：spacing.unit，
    backgroundColor：palette.background.default，
    color：palette.primary。 main，
  }，
}））;
```

這是因為TypeScript [擴展了函數表達式](https://github.com/Microsoft/TypeScript/issues/241)的返回類型。

因此，我們建議使用我們的 `createStyles` 幫助函數來構造樣式規則對象：

```ts
//非依賴樣式
常量樣式= createStyles（{
  根： {
    display: 'flex',
    flexDirection: 'column',
  }，
}）;

//依賴於主題的樣式
const styles =（{ palette, spacing }：Theme）=> createStyles（{
  root：{
    display：'flex'，
    flexDirection：'column'，
    padding：spacing.unit，
    backgroundColor：palette .background.default，
    color：palette.primary.main，
  }，
}）;
```

`createStyles` 只是身份功能;它不會在運行時“做任何事情”，只是幫助在編譯時引導類型推斷。

### 媒體查詢

`withStyles` 允許樣式對象具有頂級媒體查詢，如下所示：

```ts
常量樣式= createStyles（{
  根： {
    minHeight: '100vh',
  }，
  '@media（最小寬度：960像素）'：{
    根： {
      display: 'flex',
    }，
  }，
}）;
```

但是，為了允許這些樣式傳遞TypeScript，定義必須與CSS類的名稱和實際的CSS屬性名稱不明確。 由於此類名稱應該等於CSS屬性應該避免。

```ts
//錯誤，因為打字稿認為`@media（最小寬度：960像素）`是類名
//和`content`是CSS屬性
常量ambiguousStyles = createStyles（{
  含量： {
    minHeight: '100vh',
  }，
  '@media（分-width：960像素）'：{
    含量： {
      display: 'flex',
    }，
  }，
}）;

//工作得很好
常量ambiguousStyles = createStyles（{
  內容類： {
    minHeight: '100vh',
  }，
  '@media（最小寬度：960像素）'：{
    內容類： {
      display: 'flex',
    }，
  }，
}）;
```

### 使用 `WithStyles`道具

由於用 `withStyles（樣式）` 裝飾的組件獲得了特殊的 `類` prop注入，因此您需要相應地定義其props：

```ts
const styles =（theme：Theme）=> createStyles（{
  root：{/ * ... * /}，
  紙：{/ * ... * /}，
  按鈕：{/ * ... * /}，
}）;

界面道具{
  //非風格道具
  foo：數字;
  bar：boolean;
  //注入樣式道具
  類：{
    root：string;
    紙：字符串;
    按鈕：字符串;
  };
}
```

然而，這是不是很 [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) ，因為它需要你保持類名（`'根'`， `“紙”`， `'按鈕'`在兩個不同的地方，...）。 我們提供了一個類型操作符 `WithStyles` 來幫助解決這個問題，以便您可以編寫

```ts
從'@ material-ui / core'導入 { WithStyles, createStyles } ;

const styles =（theme：Theme）=> createStyles（{
  root：{/ * ... * /}，
  紙：{/ * ... * /}，
  按鈕：{/ * ... * /}，
}）;

接口道具擴展WithStyles<typeof styles> {
  foo：number;
  bar：boolean;
}
```

### 裝飾組件

應用 `withStyles（styles）` 作為函數按預期工作：

```tsx
const DecoratedSFC = withStyles（styles）（（{text，type，color，classes}：Props）=> （
  <Typography variant={type} color={color} classes={classes}>
    {text}
  </Typography>
））;

const DecoratedClass = withStyles（styles）（
  類擴展React.Component<Props> {
    render（）{
      const {text，type，color，classes} = this.props
      return（
        <Typography variant={type} color={color} classes={classes}>
          {text}
        </Typography>
      ）;
    }
  }
）;
```

不幸的是由於 [打字稿裝飾的電流限制](https://github.com/Microsoft/TypeScript/issues/4881)， `withStyles（樣式）` 不能被用作打字稿一個裝飾。

## 自定義 `主題`

向 `Theme`添加自定義屬性時，您可以通過利用 [Typescript的模塊擴充](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation)繼續以強類型方式使用它。

以下示例添加了一個 `appDrawer` 屬性，該屬性合併到由 `material-ui`導出的屬性中：

```ts
從'@ material-ui / core / styles / createMuiTheme'導入 { Theme } ;
來自'@ material-ui / core / styles / createBreakpoints'的 { Breakpoint } 導入{ Breakpoint } ;

聲明模塊'@ material -ui / core / styles / createMuiTheme'{
  interface Theme {
    appDrawer：{
      width：React.CSSProperties ['width']
      斷點：斷點
    }
  }
  //允許配置使用` createMuiTheme`
  接口ThemeOptions {
    appDrawer？：{
      width？：React.CSSProperties ['width']
      斷點？：Breakpoint
    }
  }
}
```

以及帶有其他默認選項的自定義主題工廠：

**./styles/createMyTheme**：

```ts
從'@ material-ui / core / styles / createMuiTheme'導入createMuiTheme， { ThemeOptions } ;

出口缺省功能createMyTheme（選項：ThemeOptions）{
  返回createMuiTheme（{
    appDrawer： {
      width: 225,
      breakpoint: 'lg',
    }，
    ...選項，
  }）
}
```

這可以像：

```ts
從'./styles/createMyTheme'導入createMyTheme;

const theme = createMyTheme（{appDrawer： { breakpoint: 'md' }}）;
```