# 測試

<p class="description">編寫測試以防止回歸併編寫更好的代碼。</p>

## 內部

我們認真對待測試。 我們已經編寫並維持 **大範圍** 的測試，所以我們可以在組件信心迭代，例如，通過提供的視覺回歸測試 [的Argos-CI](https://www.argos-ci.com/mui-org/material-ui) 已被證明是真的很有幫助。 要了解有關內部測試的更多信息，您可以查看 [README](https://github.com/mui-org/material-ui/blob/master/test/README.md)。

雖然我們已達到100％的測試覆蓋率，但我們不鼓勵用戶也這樣做。 [![覆蓋狀態](https://img.shields.io/codecov/c/github/mui-org/material-ui/master.svg)](https://codecov.io/gh/mui-org/material-ui/branch/master)

## 用戶空間

那麼在用戶空間編寫測試呢？ Material-UI樣式基礎架構使用構建在 [酶](https://github.com/airbnb/enzyme) 之上的一些輔助函數來使過程更容易，我們正在暴露。 如果您願意，可以利用它們。

### 淺呈現

淺渲染對於將測試約束為一個單元非常有用。 這還可以確保您的測試不會間接斷言子組件的行為。 創建了淺層渲染以單獨測試組件。 這意味著不會洩漏子實現細節，例如上下文。

`createShallow（）` 函數可用於此情況。 除了包裝酶API，它提供 `潛水` 和 `直到選擇` 選項。

### 完整的DOM渲染

完整DOM渲染非常適用於您可能具有可能與DOM API交互的組件或可能需要完整生命週期才能完全測試組件的用例（例如， `componentDidMount` 等）。

為這種情況提供了 `createMount（）` 函數。 除了包裝酶API之外，它還提供了 `cleanUp` 功能。

### 渲染為字符串

渲染到字符串對於測試服務器上使用的組件的行為很有用。 您可以利用此功能斷言生成的HTML字符串。

`createRender（）` 函數非常適合這種情況。 這只是酶API的別名，只是為了保持一致性而暴露。

## API

### `createShallow（[options]）=> 淺`

使用所需的上下文生成增強的淺函數。 有關 `淺` 功能的更多詳細信息，請參閱 [酶API文檔](https://airbnb.io/enzyme/docs/api/shallow.html)。

#### 參數

1. `選項` （*對象* [optional]） 
    - `options.shallow` （*Function* [optional]）：淺增強功能，默認使用 **酶**。
    - `options.untilSelector` （*String* [optional]）：遞歸淺呈現子項，直到找到提供的選擇器。 向下鑽取高階組件非常有用。
    - `options.dive` （*Boolean* [optional]）：Shallow渲染當前包裝器的一個非DOM子節點，並返回結果周圍的包裝器。
    - 其他鍵被轉發到 `enzyme.shallow（）`的options參數。

#### 返回

`淺` （*淺*）：淺函數。

#### 例子

```jsx
從'@ material-ui / core / test-utils'導入 { createShallow } ;

描述（'<MyComponent />'，（）=> {
  讓淺;

  之前（（）=> {
    淺= createShallow（）;
  }）;

  它（'應該工作'，（）=> {
    const wrapper = shallow（<MyComponent />）;
  }）;
}）;
```

### `createMount（[options]）=> mount`

使用所需的上下文生成增強的掛載功能。 有關 `mount` 功能的更多詳細信息，請參閱 [酶API文檔](https://airbnb.io/enzyme/docs/api/mount.html)。

#### 參數

1. `選項` （*對象* [optional]） 
    - `options.mount` （*Function* [optional]）：mount功能增強，默認使用 **酶**。
    - 其他鍵被轉發到 `enzyme.mount（）`的options參數。

#### 返回

`mount` （*mount*）：安裝功能。

#### 例子

```jsx
從'@ material-ui / core / test-utils'導入 { createMount } ;

描述（'<MyComponent />'，（）=> {
  let mount;

  before（（）=> {
    mount = createMount（）;
  }）;

  after（（）=> {
    mount.cleanUp（）;
  }）;

  它（'應該工作'，（）=> {
    const wrapper = mount（<MyComponent />）;
  }）;
}）;
```

### `createRender（[options]）=> 渲染`

使用所需的上下文生成渲染到字符串函數。 有關 `渲染` 功能的更多詳細信息，請參閱 [酶API文檔](https://airbnb.io/enzyme/docs/api/render.html)。

#### 參數

1. `選項` （*對象* [optional]） 
    - `options.render` （*Function* [optional]）：渲染函數增強，默認使用 **酶**。
    - 其他鍵被轉發到 `enzyme.render（）`的options參數。

#### 返回

`渲染` （*功能*）：渲染到字符串函數。

#### 例子

```jsx
從'@ material-ui / core / test-utils'導入 { createRender } ;

描述（'<MyComponent />'，（）=> {
  let render;

  before（（）=> {
    render = createRender（）;
  }）;

  it（'should work'，（）=> {
    const wrapper = render（<MyComponent />）;
  }）;
}）;
```