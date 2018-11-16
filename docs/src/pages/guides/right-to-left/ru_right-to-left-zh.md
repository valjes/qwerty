# Справа налево

<p class="description">Чтобы изменить направление компонентов Material-UI, вы должны выполнить следующие шаги.</p>

## меры

### 1. HTML

Убедитесь, что атрибут `dir` установлен на корпусе, иначе нативные компоненты сломаются:

```html
<body dir="rtl">
```

### 2. тема

Задайте направление в пользовательской теме:

```js
const theme = createMuiTheme ({
  direction: 'rtl',
});
```

### 3. JSS-РТЛ

Вам нужен этот JSS-плагин, чтобы перевернуть стили: [jss-rtl](https://github.com/alitaheri/jss-rtl).

```sh
npm install jss-rtl
```

После установки плагина в вашем проекте компоненты Material-UI по-прежнему требуют, чтобы он был загружен экземпляром jss, как описано ниже. Внутри, withStyles использует этот JSS-плагин, когда `направление: 'rtl'` задается в теме.

[CSS-in-JS-документация](/customization/css-in-js/#opting-out-of-rtl-transformation) объясняет немного больше о том, как работает этот плагин. Пойдите в плагин [README](https://github.com/alitaheri/jss-rtl) чтобы узнать больше об этом.

Создав новый экземпляр JSS с плагином, вы должны сделать его доступным для всех компонентов в дереве компонентов. JSS имеет [`JssProvider`](https://github.com/cssinjs/react-jss) компонент для этого:

```jsx
import { create } из 'jss';
import rtl из 'jss-rtl';
import JssProvider из 'response-jss / lib / JssProvider';
import { createGenerateClassName, jssPreset } из '@ material-ui / core / styles';

// Настройка JSS
const jss = create ({plugins: [... jssPreset (). Plugins, rtl ()]});

// Пользовательский генератор имен класса материала-UI.
const generateClassName = createGenerateClassName ();

функция RTL (реквизит) {
  возврат (
    <JssProvider jss={jss} generateClassName={generateClassName}>
      {props.children}
    </JssProvider>
  );
}
```

## демонстрация

*Используйте кнопку переключения направления в верхнем правом углу, чтобы перевернуть всю документацию*

{{"demo": "pages / guide / right-to-left / Direction.js"}}

## Отказ от преобразования rtl

Если вы хотите, чтобы какой-либо конкретный набор правил не подвергался трансформации `rtl` вы можете добавить `флип: false` в начале:

*Используйте кнопку переключения направления в верхнем правом углу, чтобы увидеть эффект*

{{"demo": "pages / guide / right-to-left / RtlOptOut.js", "hideEditButton": true}}