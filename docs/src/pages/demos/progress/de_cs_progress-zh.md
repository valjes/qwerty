---
title: 循環漸進，線性進展反應組件
components: CircularProgress，LinearProgress
---
# 進展

<p class="description">進度指示器表示未指定的等待時間或顯示進程的長度。</p>

[進度指示器](https://material.io/design/components/progress-indicators.html) 告知用戶正在進行的進程的狀態，例如加載應用程序，提交表單或保存更新。 他們傳達應用程序的狀態並指示可用的操作，例如用戶是否可以離開當前屏幕。

**確定** 指示器顯示操作需要多長時間。

**不確定** 指標可視化未指定的等待時間。

#### 作為一個整體進步

顯示一系列流程的進度時，請指出總體進度而不是每個活動的進度。

## 圓

[循環進度](https://material.io/design/components/progress-indicators.html#circular-progress-indicators) 支持確定和不確定的進程。

- **當指示器從0度移動到360度時，確定** 圓形指示器用顏色填充不可見的圓形軌跡。
- **不確定** 圓形指示器在沿著不可見軌道移動時增大和縮小。

### 通告不確定

{{“demo”：“pages / demos / progress / CircularIndeterminate.js”}}

### 互動整合

{{“demo”：“pages / demos / progress / CircularIntegration.js”}}

### 循環確定

{{“demo”：“pages / demos / progress / CircularDeterminate.js”}}

### 圓形靜態

{{“demo”：“pages / demos / progress / CircularStatic.js”}}

## 線性

[線性進度](https://material.io/design/components/progress-indicators.html#linear-progress-indicators) 指標。

### 線性不確定

{{“demo”：“pages / demos / progress / LinearIndeterminate.js”}}

### 線性確定

{{“demo”：“pages / demos / progress / LinearDeterminate.js”}}

### 線性緩衝區

{{“demo”：“pages / demos / progress / LinearBuffer.js”}}

### 線性查詢

{{“demo”：“pages / demos / progress / LinearQuery.js”}}

## 非標範圍

進度組件接受0到100範圍內的值。 這簡化了屏幕閱讀器用戶的工作，這些用戶是默認的最小/最大值。 但是，有時您可能正在處理數值源，其中值超出此範圍。 以下是如何輕鬆地將任意範圍內的值轉換為0 - 100的範圍：

```jsx
// MIN =最小期望值
// MAX = Maximium期望值

//標準化值的函數（MIN / MAX可以積分）
const normalize = value => （value  -  MIN）* 100 /（MAX  -  MIN ）;

//在渲染點使用`normalise`函數的示例組件。
功能進度（道具）{
  返回（
    <React.Fragment>
      <CircularProgress variant="determinate" value={normalise(props.value)} />
      <LinearProgress variant="determinate" value={normalise(props.value)} />
    </React.Fragment>
  ）
}
```

## 延遲外觀

圍繞響應時間有 [3個重要限制](https://www.nngroup.com/articles/response-times-3-important-limits/)。 `ButtonBase` 組件的連鎖效果可確保用戶感覺系統即時響應。 通常，在超過0.1但小於1.0秒的延遲期間不需要特殊反饋。 1.0秒後，您可以顯示一個加載程序，以保持用戶的思維流不受干擾。

{{“demo”：“pages / demos / progress / DelayingAppearance.js”}}

## 限制

在高負載下，您可能會丟失筆觸虛線動畫或查看隨機的CircularProgress環寬度。 您應該在Web worker或批處理中運行處理器密集型操作，以便不阻止主渲染線程。

![重物](/static/images/progress/heavy-load.gif)

請參閱https://github.com/mui-org/material-ui/issues/10327