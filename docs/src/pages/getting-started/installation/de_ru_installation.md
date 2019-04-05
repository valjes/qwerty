# Монтаж

<p class="description">Установите Material-UI, самый популярный в мире интерфейс React UI.</p>

Material-UI доступен как пакет [npm](https://www.npmjs.com/package/@material-ui/core).

## НПМ

Чтобы установить и сохранить в своих `зависимостях package.json` , запустите:

```sh
npm install @ material-ui / core
```

Обратите внимание, что [реагирует](https://www.npmjs.com/package/react) > = 16.3.0 и [реагирует на](https://www.npmjs.com/package/react-dom) > = 16.3.0 равными зависимостями.

## Шрифт Roboto

Material-UI был разработан с учетом шрифта [Roboto](https://fonts.google.com/specimen/Roboto) . Поэтому обязательно следуйте [эти инструкции](/style/typography/#general). Например, через Google Web Fonts:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500">
```

## Иконки шрифтов

Чтобы использовать компонент шрифта `Icon` вы должны сначала добавить шрифт [Material icons](https://material.io/tools/icons/). Вот [некоторые инструкции](/style/icons/#font-icons) о том , как сделать это. Например, через Google Web Fonts:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

## Значки SVG

Для того , чтобы использовать прекомпилированную SVG Материал иконку, такие как те , которые найдены в [компонентных демках](/demos/app-bar/) вы должны сначала установить [@ материал-UI / иконок](https://www.npmjs.com/package@material-ui/icons) пакета:

```sh
npm install @ material-ui / icons
```

## CDN

Вы можете начать использовать Material-UI с минимальной инфраструктурой Front-end, которая отлично подходит для прототипирования. Мы препятствуем использованию этого подхода в производстве, хотя - клиент должен загружать всю библиотеку, независимо от того, какие компоненты фактически используются, влияет на производительность и использование полосы пропускания.

#### Выпуски UMD

Мы предоставляем два файла Universal Mod Definition (UMD):

- один для разработки: https://unpkg.com/@material-ui/core/umd/material-ui.development.js
- один для производства: https://unpkg.com/@material-ui/core/umd/material-ui.production.min.js

Вы можете следить за [этот пример CDN](https://github.com/mui-org/material-ui/tree/master/examples/cdn) , чтобы быстро начать работу.