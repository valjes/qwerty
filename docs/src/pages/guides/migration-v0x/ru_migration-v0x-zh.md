# Миграция Из v0.x

<p class="description">Да, v1 был выпущен! Воспользуйтесь преимуществами двух лет работы.</p>

## Часто задаваемые вопросы

### Woah - API отличается от других! Означает ли это, что 1.0 совершенно по-другому, мне придется сначала изучить основы, и миграция будет практически невозможна?

Я рад, что вы спросили! Ответ - нет. Основные понятия не изменились. Вы заметите, что API обеспечивает большую гибкость, но это требует затрат. Мы создаем компоненты нижнего уровня, абстрагируясь от меньшей сложности.

### Что побудило такие большие перемены?

Материал-UI был запущен [4 года назад](https://github.com/mui-org/material-ui/commit/28b768913b75752ecf9b6bb32766e27c241dbc46). С тех пор экосистема сильно изменилась, мы также многому научились. [@nathanmarks](https://github.com/nathanmarks/) начал амбициозную задачу, пересоздав Material-UI из **оснований** , воспользовавшись этими знаниями для решения долговременных проблем. Чтобы назвать некоторые из основных изменений:

- Новое решение для укладки с помощью CSS-в-JS (лучше [настройки](/customization/overrides/) мощности, более высокую производительность)
- Новые [обработки темы](/customization/themes/) (гнездование, самонесущий и т. Д.)
- Быстрая документация благодаря [Next.js](https://github.com/zeit/next.js)
- Лучше всего [охват теста](/guides/testing/) (99% +, запуск во всех основных браузерах, [визуальных регрессионных теста](https://www.argos-ci.com/mui-org/material-ui))
- Полный [серверный рендеринг](/guides/server-rendering/) поддержки
- Широкий диапазон [поддерживаемых браузеров](/getting-started/supported-platforms/)

### Где я должен начать миграцию?

1. Начните с установки версии v1.x Material-UI вдоль версии v0.x.
    
    С пряжей:
    
    ```sh
    пряжа добавить материал-ui
    пряжа добавить @ материал-ui / core
    ```
    
    Или с npm:
    
    ```sh
    npm install material-ui
    npm install @ material-ui / core
    ```
    
    затем
    
    ```js
    импортировать FlatButton из 'material-ui / FlatButton'; // v0.x
    кнопка импорта из '@ material-ui / core / Button'; // v1.x
    ```

2. Запустите [помощника по миграции](https://github.com/mui-org/material-ui/tree/master/packages/material-ui-codemod) в вашем проекте.

3. `MuiThemeProvider` является необязательным для v1.x., но если у вас есть пользовательская тема, вы можете одновременно использовать версии v0.x и v1.x компонента, например:
    
    ```jsx
    import React from 'react';
    import { MuiThemeProvider, createMuiTheme } из '@ material-ui / core / styles'; // v1.x
    import { MuiThemeProvider as V0MuiThemeProvider} из 'material-ui';
    import getMuiTheme из 'material-ui / styles / getMuiTheme';
    
    const theme = createMuiTheme ({
    / * тема для v1.x * /
    });
    const themeV0 = getMuiTheme ({
    / * тема для v0.x * /
    });
    
    function App () {
    return (
      <MuiThemeProvider theme={theme}>
        <V0MuiThemeProvider muiTheme={themeV0}>
          {/ * Компоненты * /}
        </V0MuiThemeProvider>
      </MuiThemeProvider>
    );
    }
    
    экспортное приложение по умолчанию;
    ```

4. После этого вы можете перенести один экземпляр компонента в то время.

## Компоненты

### Автозаполнение

Material-UI не предоставляет API высокого уровня для решения этой проблемы. Вам предлагается изучить [решений, созданных сообществом React](/demos/autocomplete/).

В будущем мы рассмотрим предоставление простого компонента для решения простых случаев использования: [# 9997](https://github.com/mui-org/material-ui/issues/9997).

### Иконка Svg

Запустите [помощника по миграции](https://github.com/mui-org/material-ui/tree/master/packages/material-ui-codemod) в вашем проекте.

Это применит следующее изменение:

```diff
-import AddIcon из 'material-ui / svg-icons / Add';
+ импортировать AddIcon из '@ material-ui / icons / Add';

<AddIcon />
```

### Плоская кнопка

```diff
-импорт FlatButton из 'material-ui / FlatButton';
+ кнопка импорта из '@ material-ui / core / Button';

-<FlatButton />
+<Button />
```

### Поднятая кнопка

```diff
-import RaisedButton из 'material-ui / RaisedButton';
+ кнопка импорта из '@ material-ui / core / Button';

-<RaisedButton />
+<Button variant="contained" />
```

### подзаголовок

```diff
-import Subheader из 'material-ui / Subheader';
+ импорт ListSubheader из '@ material-ui / core / ListSubheader';

-<Subheader>Sub Heading</Subheader>
+<ListSubheader>Sub Heading</ListSubheader>
```

### тумблер

```diff
-import Переключить из 'material-ui / Toggle';
+ import Переключиться с '@ material-ui / core / Switch';

-<Toggle

-  toggled={this.state.checkedA}
-  onToggle={this.handleToggle}
-/>
+<Switch
+  checked={this.state.checkedA}
+  onChange={this.handleSwitch}
+/>
```

### Пункт меню

```diff
-import MenuItem из 'material-ui / MenuItem';
+ импортировать MenuItem из '@ material-ui / core / MenuItem';

-<MenuItem primaryText="Profile" />
+<MenuItem>Профиль</MenuItem>
```

### Иконка Скриншот

```diff
-import FontIcon из 'material-ui / FontIcon';
+ import Icon из '@ material-ui / core / Icon';

-<FontIcon>дом</FontIcon>
+<Icon>дом</Icon>
```

### Круговой прогресс

```diff
-импорт CircularProgress из 'material-ui / CircularProgress';
+ импорт CircularProgress из '@ material-ui / core / CircularProgress';

-<CircularProgress mode="indeterminate" />
+<CircularProgress variant="indeterminate" />
```

### Выпадающее меню

```diff
-import DropDownMenu из 'material-ui / DropDownMenu';
+ import Выберите из '@ material-ui / core / Select';

-<DropDownMenu></DropDownMenu>
+<Select value={this.state.value}></Select>
```

### Продолжение следует…

Вы успешно перенесли свое приложение и хотите помочь сообществу? Пожалуйста, помоги нам! У нас есть открытая проблема, чтобы закончить это руководство по миграции [# 7195](https://github.com/mui-org/material-ui/issues/7195). Любой запрос на тягу приветствуется