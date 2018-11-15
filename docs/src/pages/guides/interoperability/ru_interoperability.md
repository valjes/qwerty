# Совместимость библиотеки стилей

<p class="description">В то время как простое использование решения для моделирования на основе JSS, предоставляемого Material-UI для стилизации вашего приложения, можно использовать любое решение для моделирования, которое вы предпочитаете, от простого CSS до любого количества библиотек CSS-in-JS.</p>

Это руководство предназначено для документирования наиболее популярных альтернатив но вы должны обнаружить, что используемые здесь принципы могут быть адаптированы к другим библиотекам.

Мы представили примеры для следующих решений для моделирования:

- [Сырой CSS](#raw-css)
- [Стилированные компоненты](#styled-components)
- [эмоция](#emotion)
- [Реагировать на эмоции](#react-emotion)
- [Модули CSS](#css-modules)
- [Глобальный CSS](#global-css)
- [Реагировать на JSS](#react-jss)
- [CSS для MUI webpack Loader](#css-to-mui-webpack-loader)
- [очарование](#glamor)

## Сырой CSS

Ничего необычного, просто старый CSS. Зачем изобретать колесо, когда он работает десятилетиями?

**RawCssButton.css**

```css
.button {
  background: linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%);
  border-radius: 3px;
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, .3);
}
```

**RawCssButton.js**

```jsx
import React from 'react';
кнопка импорта из '@ material-ui / core / Button';

функция RawCssButton () {
  return (
    <div>
      <Button>
        Material-UI
      </Button>
      <Button className="button">
        Raw CSS
      </Button>
    </div>
  );
}

экспорт по умолчанию RawCssButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/vmv2mz9785)

**Примечание:** JSS вводит свои стили в нижней части `<head>`. Если вы не хотите отмечать атрибуты стиля **! Important**, вам нужно изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в демо.

## Стилированные компоненты

![звезды](https://img.shields.io/github/stars/styled-components/styled-components.svg?style=social&label=Star) ![НПМ](https://img.shields.io/npm/dm/styled-components.svg?)

Метод `styleled ()` отлично работает на всех наших компонентах.

```jsx
import React from 'react';
импорт в стиле «стилизованные компоненты»;
кнопка импорта из '@ material-ui / core / Button';

const StyledButton = стиль (кнопка) `
  background: linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%);
  радиус границы: 3px;
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, .3);
`;

Функция StyledComponentsButton () {
  return (
    <div>
      <Button>
        Material-UI
      </Button>
      <StyledButton>
        Styled Components
      </StyledButton>
    </div>
  );
}

экспорт по умолчанию StyledComponentsButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/mzwqkk1p7j)

### Управление приоритетом

Оба стилизованных компонента и JSS вводят свои стили в нижней части `<head>`. Один из подходов к обеспечению стилей стильных компонентов загружается последним, чтобы изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в демо.

Другой подход состоит в том, чтобы использовать символ `&` в стилизованных компонентах до [кратной специфичности](https://www.styled-components.com/docs/advanced#issues-with-specificity) , повторяя имя класса. Используйте это, чтобы стили стилей были применены перед стилями JSS. Пример этого решения:

```jsx
import React from 'react';
импорт в стиле «стилизованные компоненты»;
кнопка импорта из '@ material-ui / core / Button';

const StyledButton = стиль (кнопка) `
  && {
    background: линейный градиент (45deg, # fe6b8b 30%, # ff8e53 90%);
    border-radius: 3px;
    граница: 0;
    цвет: белый;
    высота: 48 пикселей;
    обивка: 0 30px;
    box-shadow: 0 3px 5px 2px rgba (255, 105, 135, .3);
  }
`;

Функция StyledComponentsButton () {
  return (
    <div>
      <Button>
        Material-UI
      </Button>
      <StyledButton>
        Styled Components
      </StyledButton>
    </div>
  );
}

экспорт по умолчанию StyledComponentsButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/xpp5oj9o0z)

### Более глубокие элементы

В некоторых случаях вышеприведенные подходы не будут работать. Например, если вы попытаетесь стилизовать [ящик](/demos/drawers/) с вариантом `постоянным`, вам, вероятно, придется повлиять на стиль `листов бумаги` ящике.

Однако это не корневой элемент `Drawer` и поэтому настройка стилизованных компонентов, как указано выше, не будет работать. Вы можете обойти это, используя [стабильных имен классов JSS](/customization/css-in-js/#global-css), но самым надежным подходом является использование свойства `класса` для введения стиля переопределения, а затем его стиль с более высокой специфичностью через `&`.

Следующий пример отменяет `метки` стиль `кнопки` в дополнении к пользовательским стилям на самой кнопке. Он также работает вокруг [этой проблемы с элементами стиля](https://github.com/styled-components/styled-components/issues/439) , «потребляя» свойства, которые не должны передаваться базовому компоненту.

```jsx
import React from 'react';
импорт в стиле «стилизованные компоненты»;
кнопка импорта из '@ material-ui / core / Button';

const StyledButton = styled (({ color, ...other }) => (
  <Button {...other} classes={{ label: 'label' }} />
)) `
  background: линейный градиент (45deg, # fe6b8b 30%, # ff8e53 90%);
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, 0,3);

  & .label {
    color: $ {props => props.color};
  }
`;

Функция StyledComponentsButton () {
  return (
    <div>
      <Button>Material-UI</Button>
      <StyledButton color="papayawhip">Styled Components</StyledButton>
    </div>
  );
}

экспорт по умолчанию StyledComponentsButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/j4n13yl1r9)

## эмоция

Метод **css ()** Emotion работает без проблем с Material-UI. Имена классов , возвращаемые **CSS ()** может быть непосредственно передаются на компонент `имени класс` опору , чтобы переопределить стили корня.

```jsx
import React from 'react';
импорт { css } из 'эмоции';
кнопка импорта из '@ material-ui / core / Button';

const buttonStyles = css`
  background: linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%);
  радиус границы: 3;
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, 0,3);
`;

// Мы просто назначаем им атрибут класса ClassName Button
function EmotionButton () {
  return (
    <div>
      <Button>Material-UI</Button>
      <Button className={buttonStyles}>Emotion</Button>
    </div>
  );
}

экспорт по умолчанию EmotionButton
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/yw93kl7y0j)

### Более глубокие элементы

Стили, созданные с помощью **css ()** также могут быть сопоставлены с именами классов с использованием `классов` опоры. Это полезно, если вы хотите настроить стили более глубоких элементов внутри компонента.

```jsx
import React from 'react';
импорт { css } из 'эмоции';
кнопка импорта из '@ material-ui / core / Button';

const styles = {
  button: css ({
    background: 'linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%)',
    borderRadius: 3,
    border: 0,
    height: 48,
    padding : '0 30px',
    boxShadow: '0 3px 5px 2px rgba (255, 105, 135, 0.3)',
  }),
  label: css ({
    color: 'papayawhip',
  }),
};

функция EmotionButton () {
  return (
    <div>
      <Button>Material-UI</Button>
      <Button className={styles.button} classes={{ label: styles.label }}>
        Emotion
      </Button>
    </div>
  );
}

экспорт по умолчанию EmotionButton
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/4q8o1y975w)

**Примечание:** По умолчанию Emotion и JSS вводят свои стили в нижней части `<head>`. Если вы не хотите отмечать атрибуты стиля **! Important**, вам нужно изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в примерах.

## Реагировать на эмоции

Функция **styled ()** может использоваться для настройки корневых стилей любого компонента Material-UI.

```jsx
import React from 'react';
импорт в стиле «реакция-эмоция»;
кнопка импорта из '@ material-ui / core / Button';

const StyledButton = стиль (кнопка) `
  background: linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%);
  радиус границы: 3;
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, 0,3);
`;

Функция ReactEmotionButton () {
  return (
    <div>
      <Button>Material-UI</Button>
      <StyledButton>React Emotion</StyledButton>
    </div>
  );
}

экспорт по умолчанию ReactEmotionButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/xj81yqx504)

**Примечание:** По умолчанию Emotion и JSS вводят свои стили в нижней части `<head>`. Если вы не хотите отмечать атрибуты стиля **! Important**, вам нужно изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в примерах.

## Модули CSS

![звезды](https://img.shields.io/github/stars/css-modules/css-modules.svg?style=social&label=Star)

Трудно узнать рыночную долю [этого решения для моделирования](https://github.com/css-modules/css-modules) поскольку он зависит от того, как люди используют пакета.

**CssModulesButton.css**

```css
.button {
  background: linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%);
  border-radius: 3px;
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, .3);
}
```

**CssModulesButton.js**

```jsx
import React from 'react';
// webpack, parcel или иначе введет CSS в стили импорта страницы
из './CssModulesButton.css';
кнопка импорта из '@ material-ui / core / Button';

функция CssModulesButton () {
  return (
    <div>
      <Button>
        Material-UI
      </Button>
      <Button className={styles.button}>
        CSS-модули
      </Button>
    </div>
  );
}

экспорт по умолчанию CssModulesButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/m4j01r75wx)

**Примечание:** JSS вводит свои стили в нижней части `<head>`. Если вы не хотите отмечать атрибуты стиля **! Important**, вам нужно изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в демо.

## Глобальный CSS

Явное предоставление имен классов компоненту - это слишком много усилий? Будьте уверены, мы предоставляем возможность сделать имена классов **детерминированными** для быстрого прототипирования : [`dangerouslyUseGlobalCSS`](/customization/css-in-js/#global-css).

**GlobalCssButton.css**

```css
.MuiButton-root {
  background: linear-gradient (45deg, # fe6b8b 30%, # ff8e53 90%);
  border-radius: 3px;
  граница: 0;
  цвет: белый;
  высота: 48 пикселей;
  дополнений: 0 30px;
  box-shadow: 0 3px 5px 2px rgba (255, 105, 135, .3);
}
```

**GlobalCssButton.js**

```jsx
import React from 'react';
кнопка импорта из '@ material-ui / core / Button';

функция GlobalCssButton () {
  return (
    <div>
      <Button>
        Global CSS
      </Button>
    </div>
  );
}

экспорт по умолчанию GlobalCssButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/2zv5m0j37p)

**Примечание:** JSS вводит свои стили в нижней части `<head>`. Если вы не хотите отмечать атрибуты стиля **! Important**, вам нужно изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в демо.

## Реагировать на JSS

![звезды](https://img.shields.io/github/stars/cssinjs/jss.svg?style=social&label=Star) ![НПМ](https://img.shields.io/npm/dm/react-jss.svg?)

Решение Material-UI's styling разделяет многие строительные блоки с [-реакцией-jss](https://github.com/cssinjs/react-jss). Мы пошли вперед и разветвили проект, чтобы справиться с нашими уникальными потребностями, но мы работаем над тем, чтобы объединить изменения и исправления с Material-UI обратно в response-jss.

```jsx
import React from 'react';
import PropTypes из 'prop-types';
import importSheet из 'response-jss / lib / injectSheet';
кнопка импорта из '@ material-ui / core / Button';

const styles = {
  button: {
    background: 'linear-gradient (45deg, # FE6B8B 30%, # FF8E53 90%)',
    borderRadius: 3,
    border: 0,
    color: 'white',
    height : 48,
    padding: '0 30px',
    boxShadow: '0 3px 5px 2px rgba (255, 105, 135, .3)',
  },
};

функция ReactJssButton (реквизит) {
  return (
    <div>
      <Button>Material-UI</Button>
      <Button className={props.classes.button}>реакция-jss</Button>
    </div>
  );
}

ReactJssButton.propTypes = {
  классов: PropTypes.object.isRequired,
};

export default injectSheet (стили) (ReactJssButton);
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/219x6qqx0p)

## CSS для MUI webpack Loader

[css-to-mui-loader](https://www.npmjs.com/package/css-to-mui-loader) для webpack позволяет писать CSS, который переводится в JS для использования с компонентом более высокого порядка [`сStyles ()`](/customization/css-in-js/#withstyles-styles-options-higher-order-component). Он предоставляет несколько крючков для доступа к теме из CSS.

**webpack.config.js**

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['babel-loader', 'css-to-mui-loader']
      }
    ]
  }
}
```

**CssToMuiButton.css**

```css
.button {
  background: $(theme.palette.primary.main);
  обивка: 2su; / * Единицы измерения материала-UI * /
}

.button: hover {
  background: $(theme.palette.primary.light);
}

@media $ (theme.breakpoints.down ('sm')) {
  .button {
    font-size: $(theme.typography.caption.fontSize);
  }
}
```

**CssToMuiButton.js**

```js
import button from '@ material-ui / core / Button';
import { withStyles } из '@ material-ui / core / styles';
стиля импорта из './CssToMuiButton.css';

const CssToMuiButton = withStyles (стили) (({ classes }) => (
  <Button className={classes.button}>
    CSS для кнопки MUI
  </Button>
));
```

## очарование

![звезды](https://img.shields.io/github/stars/threepointone/glamor.svg?style=social&label=Star) ![НПМ](https://img.shields.io/npm/dm/glamor.svg?)

Хороший способ применения стилей с помощью Glamour использует функцию **css ()** а затем **класса** чтобы получить их как строки:

```jsx
import React from 'react';
импортировать гламурные из «гламурных»;
импорт { css } из «гламура»;
импортировать имена классов из «classnames»;
кнопка импорта из '@ material-ui / core / Button';

const buttonStyles = {
  background: 'linear-gradient (45deg, # FE6B8B 30%, # FF8E53 90%)',
  borderRadius: 3,
  border: 0,
  color: 'white',
  height: 48,
  padding: '0 30px',
  boxShadow: '0 3px 5px 2px rgba (255, 105, 135, .3)',
};

// Сначала мы получаем классNames с функцией glamor css.
const buttonClasses = css (buttonStyles);

// Нам нужны имена классов, которые будут строками
const className = buttonClasses.toString ();

// Затем мы просто назначаем им функцию атрибута класса ButtonName
функции GlamourButton () {
  return (
    <div>
      <Button>
        Material-UI
      </Button>
      <Button className={className}>
        Glamour
      </Button>
    </div>
  );
}

экспорт по умолчанию GlamourButton;
```

[![Кнопка редактирования](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/ov5l1j2j8z)

**Примечание:** Оба Glamour и JSS вводят свои стили в нижней части `<head>`. Если вы не хотите отмечать атрибуты стиля **! Important**, вам нужно изменить [порядок вставки CSS](/customization/css-in-js/#css-injection-order), как в демо.