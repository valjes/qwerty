---
components: Значок, SvgIcon
---
# Иконки

<p class="description">Руководство и рекомендации по использованию значков с Material-UI.</p>

Значок системы [](https://material.io/design/iconography/system-icons.html) или значок пользовательского интерфейса символизирует команду, файл, устройство или каталог. Системные значки также используются для представления общих действий, таких как «мусор», «печать» и «сохранение», и обычно встречаются в панелях приложений, панелях инструментов, кнопках и списках. Google предоставил набор [Значков материалов](https://material.io/tools/icons/?style=baseline) которые следуют этим рекомендациям.

Material-UI предоставляет два компонента для отображения системных значков: `SvgIcon` для визуализации путей SVG и `значка` для отображения значков шрифтов.

## Значки SVG

Компонент `SvgIcon` принимает в качестве дочернего элемента SVG `path` и преобразует его в компонент React, который отображает путь и позволяет значку стилизоваться и реагировать на события мыши. Элементы SVG следует масштабировать для окна просмотра 24x24px.

Результирующий значок может использоваться как есть, или включен как дочерний элемент для других компонентов Material-UI, которые используют значки. По умолчанию значок наследует текущий цвет текста. При желании вы можете установить цвет значка с помощью одного из свойств цвета темы: `первичный`, `вторичный`, `действие`, `ошибка` & `отключено`.

{{"demo": "pages / style / icons / SvgIcons.js"}}

### Значки SVG Material

Интересно иметь строительные блоки, необходимые для реализации пользовательских значков, но как насчет пресетов? Мы предоставляем отдельный пакет npm, [@ material-ui / icons](https://www.npmjs.com/package/@material-ui/icons), который включает в себя 1000+ официальных [значков материалов](https://material.io/tools/icons/?style=baseline) преобразованных в `компонентов SvgIcon`.

<a href="https://material.io/tools/icons/?icon=3d_rotation&style=baseline">
  <img src="/static/images/icons/icons.png" alt="Официальные значки материалов" style="width: 566px" />
</a>

#### использование

Вы можете использовать [material.io/tools/icons](https://material.io/tools/icons/?style=baseline) чтобы найти конкретный значок. Импортируйте значок, помните, что имена значков равны `PascalCase`, например: - [`delete`](https://material.io/tools/icons/?icon=delete&style=baseline) отображается как `@ material-ui / icons / Delete` - [`delete forever`](https://material.io/tools/icons/?icon=delete_forever&style=baseline) отображается как `@ material-ui / icons / DeleteForever`

Для *«тематического»* иконки, добавьте название темы на имя значка. Например, при значении - Обрезанный [`удалить значок`](https://material.io/tools/icons/?icon=delete&style=outline) отображается как `@ material-ui / icons / DeleteOutlined` - Значок Rounded [`delete`](https://material.io/tools/icons/?icon=delete&style=rounded) отображается как `@ material-ui / icons / DeleteRounded` - Значок «Два тона [`удалять`](https://material.io/tools/icons/?icon=delete&style=twotone) отображается как `@ material-ui / icons / DeleteTwoTone` - Значок «Sharp [`delete`](https://material.io/tools/icons/?icon=delete&style=sharp) отображается как `@ material-ui / icons / DeleteSharp`

Существует три исключения из этого правила: - [`3d_rotation`](https://material.io/tools/icons/?icon=3d_rotation&style=baseline) отображается как `@ material-ui / icons / ThreeDRotation` - [`4k`](https://material.io/tools/icons/?icon=4k&style=baseline) отображается как `@ material-ui / icons / FourK` - [`360`](https://material.io/tools/icons/?icon=360&style=baseline) выставлен как `@ material-ui / icons / ThreeSixty`

{{"demo": "pages / style / icons / SvgMaterialIcons.js"}}

#### импорт

- Если ваша среда не поддерживает дрожание дерева, **рекомендуется** способ импорта значков:

```jsx
импортировать AccessAlarmIcon из '@ material-ui / icons / AccessAlarm';
import ThreeDRotation from '@ material-ui / icons / ThreeDRotation';
```

- Если ваша среда поддерживает дрожание дерева, вы также можете импортировать значки таким образом:

```jsx
import { AccessAlarm, ThreeDRotation } из '@ material-ui / icons';
```

Примечание: Импорт именованного экспорта в этом случае приведет в коде *каждый значок* будучи включенным в проекте, поэтому не рекомендуются , если вы не настроите [дерево встряхивания](https://webpack.js.org/guides/tree-shaking/). Это может также повлиять на производительность Hot Module Update.

### Дополнительные иконки SVG

Ищете еще больше значков SVG? Есть много проектов, но [https://materialdesignicons.com](https://materialdesignicons.com/) обеспечивает более 2000 официальных и сообществ, предоставленных значками. [mdi-material-ui](https://github.com/TeamWertarbyte/mdi-material-ui) упаковывает эти значки в Material-UI SvgIcons так же, как [@ material-ui / icons](https://www.npmjs.com/package/@material-ui/icons) для официальных значков.

## Иконки шрифтов

Компонент `Icon` отобразит значок из любого шрифта значка, который поддерживает лигатуры. В качестве предварительного условия, вы должны включать в себя один, например, [Материал шрифта значок](http://google.github.io/material-design-icons/#icon-font-for-the-web) в проекте, например, с помощью Google Web Fonts:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

`Значок` установит правильное имя класса для шрифта значка материала. Для других шрифтов, вы должны указать имя класса с помощью значка компонент `Classname` недвижимости.

Чтобы использовать значок, просто оберните имя значка (лигатура шрифта) с помощью компонента `Icon` , например :

```jsx
<Icon>звезд</Icon>
```

По умолчанию значок наследует текущий цвет текста. При желании вы можете установить цвет значка с помощью одного из свойств цвета темы: `первичный`, `вторичный`, `действие`, `ошибка` & `отключено`.

### Значки материала шрифта

{{"demo": "pages / style / icons / Icons.js"}}

### Шрифт Awesome

[Шрифт Awesome](https://fontawesome.com/icons) можно использовать с компонентом `Icon` следующим образом:

{{"demo": "pages / style / icons / FontAwesome.js", "hideEditButton": true}}

## Font vs SVG. Какой подход к использованию?

Оба подхода работают хорошо, однако есть некоторые тонкие различия, особенно с точки зрения производительности и качества рендеринга. По возможности SVG является предпочтительным, поскольку он позволяет разделить код, поддерживает больше значков, делает все быстрее и лучше.

Для получения более подробной информации, вы можете проверить [почему GitHub мигрировал](https://blog.github.com/2016-02-22-delivering-octicons-with-svg/) из иконок шрифтов в иконки SVG.

## доступность

Значки могут передавать всевозможные содержательные сведения, поэтому важно, чтобы они достигли наибольшего количества людей. Вы можете рассмотреть два варианта использования: - **Декоративные значки** используются только для визуального или фирменного подкрепления. Если они будут удалены со страницы, пользователи все равно поймут и смогут использовать вашу страницу. - **Семантические значки** - это те, которые вы используете, чтобы передать смысл, а не просто чистое украшение. Сюда входят значки без текста рядом с ними, используемые в качестве интерактивных элементов управления - кнопки, элементы формы, переключатели и т. Д.

### Декоративные иконки SVG

Если ваши значки являются чисто декоративными, вы уже готовы! Мы добавляем атрибут `aria-hidden = true` чтобы ваши значки были правильно доступны (невидимы).

### Семантические значки SVG

Если значок имеет смысловое значение, все , что вам нужно сделать , это бросить в `titleAccess = «означает»` свойство. Мы добавляем атрибут `role = "img"` и элемент `<title>` чтобы ваши значки были правильно доступны.

В случае интерактивных интерактивных элементов, например, при использовании кнопки со значком, вы можете использовать свойство `aria-label`:

```jsx
import IconButton из '@ material-ui / core / IconButton';
импортировать SvgIcon из '@ material-ui / core / SvgIcon';

// ...

<IconButton aria-label="Delete">
  <SvgIcon>
    <path d="M20 12l-1.41-1.41L13 16.17V4h-2v12.17l-5.58-5.59L4 12l8 8 8-8z" />
  </SvgIcon>
</IconButton>
```

### Декоративные шрифтовые иконы

Если ваши значки являются чисто декоративными, вы уже готовы! Мы добавляем атрибут `aria-hidden = true` чтобы ваши значки были правильно доступны (невидимы).

### Иконки семантического шрифта

Если ваши значки имеют смысловое значение, вам нужно предоставить текстовую альтернативу, только видимую для усложняющих технологий.

```jsx
значок импорта из '@ material-ui / core / Icon';
import Typography от '@ material-ui / core / Typography';

// ...

<Icon>add_circle</Icon>
<Typography variant="srOnly">Создать пользователя</Typography>
```

### Ссылка

- https://developer.paciellogroup.com/blog/2013/12/using-aria-enhance-svg-accessibility/