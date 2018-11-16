# CSS в JS

<p class="description">即使 您 没有 使用 我们 的 组件, 您 也 可以 利用 我们 的 造型 解决 方案.</p>

Material-UI нацелен на создание прочных основ для создания динамических пользовательских интерфейсов. Для простоты, **мы разоблачим наше решение для стилей для пользователей**. Вы можете использовать его, но вам этого не нужно. Это решение для моделирования является [совместимым с](/guides/interoperability/) всеми другими основными решениями.

## Решение для моделирования материала-UI

В предыдущих версиях Material-UI использовал LESS, а затем пользовательское встроенное решение для написания стиля компонентов, но эти подходы оказались ограниченными. Совсем недавно, мы имеем [перемещается к](https://github.com/oliviertassinari/a-journey-toward-better-style) *CSS-в-JS* раствора. Он **разблокирует множество замечательных функций** (тематическое вложение, динамические стили, самоподдержка и т. Д.). Мы считаем, что это будущее:

- [Единый язык стилизации](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660)
- [Будущее компоновки на основе компонентов](https://medium.freecodecamp.org/css-in-javascript-the-future-of-component-based-styling-70b161a79a32)
- [Преобразование SCSS (Sass) в CSS-in-JS](https://egghead.io/courses/convert-scss-sass-to-css-in-js)

Таким образом, вы , возможно, заметили в демоса , что *CSS-в-JS* выглядит. Мы используем компонент более высокого порядка, созданный с помощью [`withStyles`](#api) чтобы ввести массив стилей в DOM как CSS, используя JSS. Вот пример:

{{"demo": "pages / customization / css-in-js / CssInJs.js"}}

## JSS

Решение для моделирования материала-UI использует [JSS](https://github.com/cssinjs/jss) по своему ядру. Это [высокой производительности](https://github.com/cssinjs/jss/blob/master/docs/performance.md) JS для компилятора CSS , который работает во время выполнения и на стороне сервера. Это около 8 кБ (минимизировано и gzipped) и расширяемо через API-интерфейсы [plugins](https://github.com/cssinjs/jss/blob/master/docs/plugins.md).

Если вы в конечном итоге с помощью этого стайлинга решение в вашем коде, вы будете нуждаться в *изучить API*. Самое лучшее место для начала, глядя на особенности , что каждый [плагин](http://cssinjs.org/plugins/) обеспечивает. Material-UI использует [из них](#plugins). Вы всегда можете добавить новые плагины, если необходимо, с помощью помощника [`JssProvider`](https://github.com/cssinjs/react-jss#custom-setup).

Если вы хотите создать свой собственный экземпляр `jss` **и** поддержите *rtl* убедитесь, что вы также включили [jss-rtl](https://github.com/alitaheri/jss-rtl) плагин. Проверьте jss-rtl [readme](https://github.com/alitaheri/jss-rtl#simple-usage) чтобы узнать, как это сделать.

## Реестр ведомостей

При рендеринге на сервере вам нужно будет получить все отображаемые стили в виде строки CSS. Класс `SheetsRegistry` позволяет вручную группировать и строгать их. Подробнее о [серверах Rendering](/guides/server-rendering/).

{{"demo": "pages / customization / css-in-js / JssRegistry.js", "hideEditButton": true}}

## Менеджер листов

Менеджер листов использует [подсчет ссылочный](https://en.wikipedia.org/wiki/Reference_counting) алгоритм для того , чтобы прикрепиться и разделиться таблицы стилей только один раз в (стили, темы) пара. Этот метод обеспечивает значительное повышение производительности при повторной передаче экземпляров компонента.

Когда только рендеринг на клиенте, это не то, о чем вам нужно знать. Однако при рендеринге на сервере вы это делаете. Вы можете узнать больше о [Server Rendering](/guides/server-rendering/).

## Названия классов

Возможно, вы заметили, что имена классов, сгенерированные нашим решением для стилизации, являются **недетерминированными**, поэтому вы не можете полагаться на них, чтобы оставаться неизменными. Следующий CSS не будет работать:

```css
.MuiAppBar-root-12 {
  opacity: 0.6
}
```

Вместо этого вы должны использовать свойство `классов` компонента для их переопределения. С другой стороны, благодаря неопределенному характеру имен наших классов мы можем реализовать оптимизацию для разработки и производства. Они легко отлаживаются в разработке и как можно короче в производстве:

- разработка: `.MuiAppBar-root-12`
- производство: `.jss12`

Если вам не нравится это поведение по умолчанию, вы можете его изменить. JSS опирается на концепцию [класса имя генератора](http://cssinjs.org/js-api/#generate-your-own-class-names).

### Глобальный CSS

Мы предоставляем пользовательскую реализацию генератора имен классов для потребностей Material-UI: [`createGenerateClassName ()`](#creategenerateclassname-options-class-name-generator). А также возможность сделать имена классов **детерминированными** с `опасноUseGlobalCSS`. При включении имена классов будут выглядеть так:

- разработка: `.MuiAppBar-root`
- производство: `.MuiAppBar-root`

⚠️ **Будьте осторожны при использовании `опасноUseGlobalCSS`.** Мы предоставляем эту опцию в качестве защитного люка для быстрого прототипирования. Опираясь на это для запуска кода в производстве имеет следующие последствия:

- Глобальный CSS по своей сути является хрупким. Люди используют строгие методологии, такие как [BEM](http://getbem.com/introduction/) для решения проблемы.
- Сложнее отслеживать изменения API-интерфейсов `классов`.

⚠️ При использовании `опасноUseGlobalCSS` автономно (без Material-UI), вы должны назвать свои таблицы стилей. `withStyles` имеет для этого параметр имени:

```jsx
const Button = withStyles (стили, { name: 'button' }) (ButtonBase)
```

## Порядок вставки CSS

CSS, введенный Material-UI для стилизации компонента, имеет самую высокую специфичность, поскольку `<link>` вводится в нижней части `<head>` чтобы гарантировать, что компоненты всегда отображаются правильно.

Однако вы можете также переопределить эти стили, например, с помощью стилизованных компонентов. Если вы столкнулись с проблемой заказа на поставку CSS, JSS [предоставляет механизм](https://github.com/cssinjs/jss/blob/master/docs/setup.md#specify-dom-insertion-point) для обработки этой ситуации. Регулируя размещение `ТочкаВставки` в вашем HTML голове вы можете [контролировать порядок](http://cssinjs.org/js-api/#attach-style-sheets-in-a-specific-order) , что правила CSS применяются к компонентам.

### Комментарий HTML

Самый простой подход - добавить комментарий HTML, который определяет, где JSS будет вводить стили:

```jsx
<head>
  <! - jss-insertion-point ->
  <link href="..." />
</head>
```

```jsx
импортировать JssProvider из 'response-jss / lib / JssProvider';
import { create } из 'jss';
import { createGenerateClassName, jssPreset } из '@ material-ui / core / styles';

const generateClassName = createGenerateClassName ();
const jss = create ({
  ... jssPreset (),
  // Мы определяем настраиваемую точку вставки, которую JSS будет искать для вставки стилей в DOM.
  insertionPoint: 'jss-insertion-point',
});

функция App () {
  return (
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  );
}

экспортное приложение по умолчанию;
```

### Другой элемент HTML

[Create React App](https://github.com/facebook/create-react-app) разбивает комментарии HTML при создании сборки сборки. Чтобы обойти эту проблему, вы можете указать элемент DOM (кроме комментария) в качестве точки вставки JSS.

Например, элемент `<noscript>`:

```jsx
<head>
  <noscript id="jss-insertion-point"></noscript>
  <link href="..." />
</head>
```

```jsx
импортировать JssProvider из 'response-jss / lib / JssProvider';
import { create } из 'jss';
import { createGenerateClassName, jssPreset } из '@ material-ui / core / styles';

const generateClassName = createGenerateClassName ();
const jss = create ({
  ... jssPreset (),
  // Мы определяем настраиваемую точку вставки, которую JSS будет искать для вставки стилей в DOM.
  insertionPoint: document.getElementById ('jss-insertion-point'),
});

функция App () {
  return (
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  );
}

экспортное приложение по умолчанию;
```

### JS createComment

codesandbox.io предотвращает доступ к элементу `<head>`. Чтобы обойти эту проблему, вы можете использовать JavaScript `document.createComment ()` API:

```jsx
импортировать JssProvider из 'response-jss / lib / JssProvider';
import { create } из 'jss';
import { createGenerateClassName, jssPreset } из '@ material-ui / core / styles';

const styleNode = document.createComment ("jss-insertion-point");
document.head.insertBefore (styleNode, document.head.firstChild);

const generateClassName = createGenerateClassName ();
const jss = create ({
  ... jssPreset (),
  // Мы определяем настраиваемую точку вставки, которую JSS будет искать для вставки стилей в DOM.
  insertionPoint: 'jss-insertion-point',
});

функция App () {
  return (
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  );
}

экспортное приложение по умолчанию;
```

## JssProvider

response-jss предоставляет компонент `JssProvider` для настройки JSS для базовых дочерних компонентов. Существуют различные варианты использования:

- Предоставление генератора имен классов.
- [Предоставление реестра листов.](/customization/css-in-js/#sheets-registry)
- Предоставление экземпляра JSS. Возможно, вы захотите поддержать [справа налево](/guides/right-to-left/) или изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order). Прочтите [документацию JSS](http://cssinjs.org/js-api/) чтобы узнать больше о доступных параметрах. Вот пример:

```jsx
импортировать JssProvider из 'response-jss / lib / JssProvider';
import { create } из 'jss';
import { createGenerateClassName, jssPreset } из '@ material-ui / core / styles';

const generateClassName = createGenerateClassName ();
const jss = create (jssPreset ());

функция App () {
  return (
    <JssProvider jss={jss} generateClassName={generateClassName}>
...
    </JssProvider>
  );
}

экспортное приложение по умолчанию;
```

## Плагины

JSS использует концепцию плагинов для расширения своего ядра, позволяя людям зависеть от функций, которые им нужны. Вы оплачиваете накладные расходы только за то, что используете. Учитывая, что `withStyles` является нашим внутренним решением для моделирования, все плагины недоступны по умолчанию. Мы добавили следующий список:

- [JSS-глобальный](http://cssinjs.org/jss-global/)
- [JSS-вложенными](http://cssinjs.org/jss-nested/)
- [JSS-верблюд случай](http://cssinjs.org/jss-camel-case/)
- [JSS-умолчанию-блок](http://cssinjs.org/jss-default-unit/)
- [JSS-поставщика prefixer](http://cssinjs.org/jss-vendor-prefixer/)
- [JSS-реквизит сортировка](http://cssinjs.org/jss-props-sort/)

Это подмножество [jss-preset-default](http://cssinjs.org/jss-preset-default/). Конечно, вы можете добавить новый плагин. Мы имеем один пример для [`JSS-РТЛ` плагина](/guides/right-to-left/#3-jss-rtl).

## API

### `withStyles (styles, [options]) => компонент более высокого порядка`

Свяжите таблицу стилей с компонентом. Он не изменяет переданный ему компонент; вместо этого он возвращает новый компонент с свойством `классов`. Этот объект `классов` содержит имя названий классов, введенных в DOM.

Некоторые детали реализации, которые могут быть интересны для понимания:

- Он добавляет свойство `классов` чтобы вы могли переопределить введенные имена классов извне.
- Он добавляет свойство `innerRef` поэтому вы можете получить ссылку на обернутый компонент. Использование `innerRef` идентично `ref`.
- Он перенаправляет *не React static* свойств, поэтому этот HOC является более «прозрачным». Например, он может быть использован для определен `getInitialProps ()` статический метод (next.js).

#### аргументы

1. `стилей` (*Функция | Объект*): функция, генерирующая стили или объект стилей. Он будет связан с компонентом. Используйте подпись функции, если вам нужен доступ к теме. Это первый аргумент.
2. `опции` (*Объект* [optional]): 
    - `options.withTheme` (*Boolean* [optional]): По умолчанию `false`. Предоставьте объект `темы` компоненту как свойство.
    - `options.name` (*String* [optional]): имя таблицы стилей. Полезно для отладки. Если значение не указано, оно попытается отступить от имени компонента.
    - `options.flip` (*Boolean* [optional]): если установлено значение `false`, этот лист откажется от преобразования `rtl`. Когда установлено значение `true`, стили обращаются. Если установлено значение `null`, это означает `theme.direction`.
    - Другие ключи пересылаются в аргумент options [jss.createStyleSheet ([styles], [options])](http://cssinjs.org/js-api/#create-style-sheet).

#### Возвращает

`компонент более высокого порядка`: следует использовать для обертывания компонента.

#### Примеры

```jsx
import { withStyles } из '@ material-ui / core / styles';

const styles = {
  root: {
    backgroundColor: 'red',
  },
};

класс MyComponent расширяет React.Component {
  render () {
    return <div className={this.props.classes.root} />;
  }
}

экспорт по умолчанию withStyles (styles) (MyComponent);
```

Кроме того, вы можете использовать как [декораторов](https://babeljs.io/docs/en/babel-plugin-proposal-decorators) так:

```jsx
import { withStyles } из '@ material-ui / core / styles';

const styles = {
  root: {
    backgroundColor: 'red',
  },
};

@withStyles (стили)
класс MyComponent расширяет React.Component {
  render () {
    return <div className={this.props.classes.root} />;
  }
}

экспорт по умолчанию MyComponent
```

### `createGenerateClassName ([options]) => генератор имен классов`

Функция, которая возвращает [функцию генератора имен классов](http://cssinjs.org/js-api/#generate-your-own-class-names).

#### аргументы

1. `опции` (*Объект* [optional]): 
    - `options.dangerouslyUseGlobalCSS` (*Boolean* [optional]): По умолчанию `false`. Делает имена класса Material-UI детерминированными.
    - `options.productionPrefix` (*String* [optional]): По умолчанию `'jss'`. Строка, используемая для префикса имен классов в процессе производства.
    - `options.seed` (*String* [optional]): По умолчанию `''`. Строка, используемая для однозначной идентификации генератора. Его можно использовать, чтобы избежать конфликтов имен классов при использовании нескольких генераторов.

#### Возвращает

`генератор имен классов`: генератор должен быть предоставлен JSS.

#### Примеры

```jsx
импортировать JssProvider из 'response-jss / lib / JssProvider';
import { createGenerateClassName } из '@ material-ui / core / styles';

const generateClassName = createGenerateClassName ({
  dangerouslyUseGlobalCSS: true,
  productionPrefix: 'c',
});

функция App () {
  return (
    <JssProvider generateClassName={generateClassName}>
...
    </JssProvider>
  );
}

экспортное приложение по умолчанию;
```

## Альтернативные API

Считаете ли вы, что [компонентов более высокого порядка являются новыми mixins](https://cdb.reacttraining.com/use-a-render-prop-50de598f11ce)? Будьте уверены, мы этого не сделаем, однако, поскольку `withStyles ()` является компонентом более высокого порядка, его можно расширить только с помощью **строк кода** чтобы соответствовать различным шаблонам, которые являются идиоматическим Реагированием. Вот несколько примеров.

### Render props API (+11 строк)

Термин [«render prop»](https://reactjs.org/docs/render-props.html) относится к простой методике совместного использования кода между компонентами React с использованием prop, значение которого является функцией.

```jsx
// Вы найдете реализацию `createStyled` в источнике демонстрации.
const Styled = createStyled ({
  root: {
    background: 'linear-gradient (45deg, # FE6B8B 30%, # FF8E53 90%)',
    borderRadius: 3,
    border: 0,
    color: 'white',
    height: 48,
    padding: '0 30px',
    boxShadow: '0 3px 5px 2px rgba (255, 105, 135, .3)',
  },
});

функция RenderProps () {
  return (
    <Styled>
      {({ classes }) => (
        <Button className={classes.root}>
          {'Render props'}
        </Button>
      )}
    </Styled>
  );
}
```

{{"demo": "pages / customization / css-in-js / RenderProps.js"}}

Вы можете получить доступ к теме так же, как и с помощью `withStyles`:

```js
const Styled = createStyled (тема => ({
  корень: {
    backgroundColor: theme.palette.background.paper,
  },
}));
```

[@ jedwards1211](https://github.com/jedwards1211) Потрачено время, чтобы переместить этот модуль в пакет: [материала-ui-render-реквизит-стили](https://github.com/jcoreio/material-ui-render-props-styles). Не стесняйтесь использовать его.

### API стильных компонентов (+15 строк)

API стилизованных компонентов удаляет сопоставление между компонентами и стилями. Использование компонентов в качестве структуры стилей низкого уровня может быть проще.

```jsx
// Вы найдете «стилизованную» реализацию в источнике демонстрации.
// Вы даже можете писать CSS с помощью https://github.com/cssinjs/jss-template.
const MyButton = style (Button) ({
  background: 'linear-gradient (45deg, # FE6B8B 30%, # FF8E53 90%)',
  borderRadius: 3,
  border: 0,
  color: 'white',
  height : 48,
  padding: '0 30px',
  boxShadow: '0 3px 5px 2px rgba (255, 105, 135, .3)',
});

функция StyledComponents () {
  return <MyButton>{'Styled Components'}</MyButton>;
}
```

{{"demo": "pages / customization / css-in-js / StyledComponents.js"}}

Вы можете получить доступ к теме так же, как и с помощью `withStyles`:

```js
const MyButton = стиль (кнопка) (тема => ({
  backgroundColor: theme.palette.background.paper,
}));
```