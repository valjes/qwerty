# Резервное копирование сервера

<p class="description">Наиболее распространенным вариантом использования для рендеринга на стороне сервера является обработка первоначального рендеринга, когда пользователь (или искатель поисковой системы) сначала запрашивает ваше приложение.</p>

Когда сервер получает запрос, он отображает требуемый компонент (ы) в строку HTML и затем отправляет его как ответ клиенту. С этого момента клиент берет на себя обязанности по предоставлению услуг.

## Material-UI на сервере

Material-UI был разработан с нуля с ограничением рендеринга на Сервере, но вам решать, чтобы он был правильно интегрирован. Важно предоставить страницу требуемому CSS, иначе страница будет отображаться только с помощью HTML, а затем ждать, пока CSS будет введена клиентом, что вызовет мерцание. Чтобы добавить стиль к клиенту, нам необходимо:

1. Создайте новый, новый экземпляр `листовRegistry` и `theme` для каждого запроса.
2. Выделите дерево React с API-интерфейсом на стороне сервера и экземпляром.
3. Вытяните CSS из `листовRegistry`.
4. Передайте CSS вместе с клиентом.

На стороне клиента CSS будет введена во второй раз, прежде чем удалять на стороне сервера CSS.

## Настройка

В следующем рецепте мы рассмотрим, как настроить рендеринг на стороне сервера.

### Серверная сторона

Ниже приведена схема того, как будет выглядеть наша серверная сторона. Мы собираемся создать [Экспресс промежуточного слоя](http://expressjs.com/en/guide/using-middleware.html) с использованием [app.use](http://expressjs.com/en/api.html) для обработки всех запросов , которые приходят в наш сервер. Если вы не знакомы с Express или промежуточным программным обеспечением, просто знайте, что наша функция handleRender будет вызываться каждый раз, когда сервер получает запрос.

`server.js`

```js
импортировать экспресс из «экспресс»;
import Реагировать с «реагировать»;
импортировать приложение из './App';

// Мы собираемся заполнить их в следующих разделах.
function renderFullPage (html, css) {
  / * ... * /
}

функция handleRender (req, res) {
  / * ... * /
}

const app = express ();

// Это запускается каждый раз, когда серверная сторона получает запрос.
app.use (handleRender);

const port = 3000;
app.listen (порт);
```

### Обработка запроса

Первое, что нам нужно сделать по каждому запросу, - создать новый экземпляр `листовRegistry` и `theme`.

При рендеринге мы обернем `App`, наш корневой компонент, внутри `JssProvider` и [`MuiThemeProvider`](/api/mui-theme-provider/) чтобы сделать `листовRegistry` и `theme` доступными для всех компонентов в дереве компонентов.

Ключевым шагом в рендеринге стороны сервера является визуализация исходного HTML нашего компонента **до** мы отправляем на клиентскую сторону. Для этого мы используем [ReactDOMServer.renderToString ()](https://reactjs.org/docs/react-dom-server.html).

Затем мы получаем CSS из нашего `sheetRegistry` используя `листаRegistry.toString ()`. Мы увидим , как это проходит вперед в нашей `renderFullPage` функцию.

```jsx
импортировать ReactDOMServer из «реактора / сервера»
import { SheetsRegistry } из «jss»;
import JssProvider из 'response-jss / lib / JssProvider';
import {
  MuiThemeProvider,
  createMuiTheme,
  createGenerateClassName,
} из '@ material-ui / core / styles';
импортировать зеленый цвет из '@ material-ui / core / colors / green';
импортировать красный цвет из '@ material-ui / core / colors / red';

function handleRender (req, res) {
  // Создаем экземпляр SheetRegistry.
  const sheetsRegistry = new SheetsRegistry ();

  // Создаем экземпляр sheetManager.
  const sheetsManager = new Map ();

  // Создаем экземпляр темы.
  const theme = createMuiTheme ({
    палитры: {
      первичный: зеленый,
      акцент: красный,
      типа: «свет»,
    },
  });

  // Создаем новый генератор имен классов.
  const generateClassName = createGenerateClassName ();

  // Передача компонента в строку.
  const html = ReactDOMServer.renderToString (
    <JssProvider registry={sheetsRegistry} generateClassName={generateClassName}>
      <MuiThemeProvider theme={theme} sheetsManager={sheetsManager}>
        <App />
      </MuiThemeProvider>
    </JssProvider>
  )

  // Возьмите CSS из наших листовRegistry.
  const css = sheetsRegistry.toString ()

  // Отправлять возвращенную страницу клиенту.
  res.send (renderFullPage (html, css))
}
```

### Вставить исходный компонент HTML и CSS

Последним шагом на стороне сервера является внедрение нашего исходного компонента HTML и CSS в шаблон, который будет отображаться на стороне клиента.

```js
Функция renderFullPage (HTML, CSS) {
  возвращение `
    <! DOCTYPE HTML>
    <html>
      <head>
        <title>Материал-интерфейса</title>
      </head>
      <body>
        <div id="root">${html}</div>
        <style id="jss-server-side">${css}</style>
      </body>
    </html>
  ';
}
```

### Сторона клиента

Клиентская сторона проста. Все, что нам нужно сделать, это удалить созданный на стороне сервера CSS. Давайте посмотрим на наш клиентский файл:

`client.js`

```jsx
import React from 'react';
import ReactDOM из «реагирования»;
import JssProvider из 'response-jss / lib / JssProvider';
import {
  MuiThemeProvider,
  createMuiTheme,
  createGenerateClassName,
} из '@ material-ui / core / styles';
импортировать зеленый цвет из '@ material-ui / core / colors / green';
импортировать красный цвет из '@ material-ui / core / colors / red';
импортировать приложение из. ./App;

класс Main extends React.Component {
  // Удаляет загруженный на стороне сервера CSS.
  componentDidMount () {
    const jssStyles = document.getElementById ('jss-server-side');
    if (jssStyles && jssStyles.parentNode) {
      jssStyles.parentNode.removeChild (jssStyles);
    }
  }

  render () {
    return <App />
  }
}

// Создаем экземпляр темы.
const theme = createMuiTheme ({
  палитры: {
    первичный: зеленый,
    акцент: красный,
    типа: «свет»,
  },
});

// Создаем новый генератор имен классов.
const generateClassName = createGenerateClassName ();

ReactDOM.hydrate (
  <JssProvider generateClassName={generateClassName}>
    <MuiThemeProvider theme={theme}>
      <Main />
    </MuiThemeProvider>
  </JssProvider>,
  document.querySelector ('# root'),
);
```

## Референсные реализации

Мы размещаем различные эталонные реализации , которые вы можете найти в [хранилище GitHub](https://github.com/mui-org/material-ui) по [`/ примерам`](https://github.com/mui-org/material-ui/tree/master/examples) папок:

- [Эталонная реализация этого учебника](https://github.com/mui-org/material-ui/tree/master/examples/ssr)
- [Next.js](https://github.com/mui-org/material-ui/tree/master/examples/nextjs)
- [Гэтсби](https://github.com/mui-org/material-ui/tree/master/examples/gatsby)

## Поиск проблемы

Если это не сработает, в 99% случаев это проблема конфигурации. Отсутствующее свойство, неправильный порядок вызова или недостающий компонент. Мы очень строгие в настройке, и лучший способ узнать, что не так, - сравнить ваш проект с уже работающей настройкой, проверить наши [эталонных реализаций](#reference-implementations), по-бит.

### CSS работает только при первой загрузке, тогда отсутствует

CSS создается только при первом загрузке страницы. Затем CSS отсутствует на сервере для последовательных запросов.

#### Действия

Мы полагаемся на кеш, менеджер листов, чтобы вводить CSS только один раз для каждого типа компонента (если вы используете две кнопки, вам нужно только один раз CSS). Вам необходимо предоставить **новый `листManager` для каждого запроса**.

Вы можете узнать больше о [концепции листов менеджера в документации](/customization/css-in-js/#sheets-manager).

*пример исправления:*

```diff
// Создаем экземпляр sheetManager.
-const sheetsManager = new Map ();

function handleRender (req, res) {

+ // Создает экземпляр sheetManager.
+ const sheetsManager = new Map ();

  // ...

  // Отметить компонент в строке.
  const html = ReactDOMServer.renderToString (
```

### Сопротивление гидратации

Между клиентом и сервером существует несоответствие имени класса. Он может работать для первого запроса. Другим симптомом является то, что стиль изменяет начальную загрузку страницы и загрузку клиентских скриптов.

#### Действия

Значение имен классов опирается на концепцию [класса имя генератора](/customization/css-in-js/#creategenerateclassname-options-class-name-generator). Вся страница должна отображаться с помощью **одиночного генератора**. Этот генератор должен вести себя одинаково на сервере и на клиенте. Например:

- Для каждого запроса необходимо предоставить генератор имен классов. Но вы можете делиться `createGenerateClassName ()` между разными запросами:

*пример исправления:*

```diff
- // Создаем новый генератор имен классов.
-const generateClassName = createGenerateClassName ();

function handleRender (req, res) {

+ // Создайте новый генератор имен классов.
+ const generateClassName = createGenerateClassName ();

  // ...

  // Отметить компонент в строке.
  const html = ReactDOMServer.renderToString (
```

- Вам нужно убедиться, что ваш клиент и сервер работают с **точно такой же версией** Material-UI. Возможно, что несоответствие даже второстепенных версий может вызвать проблемы с дизайном. Чтобы проверить номера версий, запустите `npm list @ material-ui / core` в среде, где вы создаете приложение, а также в своей среде развертывания.
    
    Вы также можете обеспечить ту же версию в разных средах, указав конкретную версию MUI в зависимостях вашего package.json.

*пример исправления (package.json):*

```diff
  "зависимости": {
...

- "@ material-ui / core": "^ 1.4.2",
+ "@ material-ui / core": "1.4.3",
...
  },
```

- Вы должны убедиться, что сервер и клиент имеют одинаковое значение `process.env.NODE_ENV`.