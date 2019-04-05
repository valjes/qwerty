# Машинопись

<p class="description">Вы можете добавить статическую типизацию в JavaScript для повышения производительности и качества кода благодаря использованию TypeScript.</p>

Посмотрите приложение [Create React с примером TypeScript](https://github.com/mui-org/material-ui/tree/master/examples/create-react-app-with-typescript). Требуется минимальная версия TypeScript 2.8.

Наши определения тестируются со следующими [tsconfig.json](https://github.com/mui-org/material-ui/tree/master/tsconfig.json). Использование менее строгих `tsconfig.json` или отсутствие некоторых библиотек может привести к ошибкам.

## Использование `withStyles`

Использование `сStyles` в TypeScript может быть немного сложным, но есть некоторые утилиты, чтобы сделать этот процесс настолько безболезненным, насколько это возможно.

### Использование `createStyles` для преодоления расширения типа

Частым источником путаницы машинопись в [тип уширение](https://blog.mariusschulz.com/2017/02/04/typescript-2-1-literal-type-widening), что приводит этот пример не работает , как ожидалось:

```ts
const styles = {
  root: {
    display: 'flex',
    flexDirection: 'column',
  }
};

withStyles (стили);
// ^^^^^^
// Типы свойства 'flexDirection' несовместимы.
// Тип 'string' не присваивается типу '' -moz-initial '| "inherit" | «начальный» | «вернуться» | «unset» | "column" | "column-reverse" | "строка"...'.
```

Проблема в том, что тип свойства `flexDirection` выводится как `строка`, что слишком произвольно. Чтобы исправить это, вы можете передать объект styles непосредственно в `withStyles`:

```ts
withStyles ({
  корень: {
    display: 'flex',
    flexDirection: 'column',
  },
});
```

Однако расширение типа возвращает его уродливую голову еще раз, если вы попытаетесь сделать стили зависеть от темы:

```ts
withStyles (({ palette, spacing }) => ({
  root: {
    display: 'flex',
    flexDirection: 'column',
    padding: spacing.unit,
    backgroundColor: palette.background.default,
    color: palette.primary. main,
  },
}));
```

Это связано с тем, что TypeScript [расширяет возвращаемые типы выражений функций](https://github.com/Microsoft/TypeScript/issues/241).

Из - за этого, мы рекомендуем использовать `createStyles` вспомогательную функцию для создания объекта ваши правила стиля:

```ts
// Независимые стили
const styles = createStyles ({
  корень: {
    display: 'flex',
    flexDirection: 'column',
  },
});

// Тематические стили
const styles = ({ palette, spacing }: Тема) => createStyles ({
  root: {
    display: 'flex',
    flexDirection: 'column',
    padding: spacing.unit,
    backgroundColor: palette .background.default,
    color: palette.primary.main,
  },
});
```

`createStyles` - это только функция идентификации; он не «ничего делать» во время выполнения, просто помогает определять вывод типа во время компиляции.

### Запросы СМИ

`withStyles` разрешает объект стилей с медиа-запросами верхнего уровня, например:

```ts
const styles = createStyles ({
  root: {
    minHeight: '100vh',
  },
  '@media (min-width: 960px)': {
    root: {
      display: 'flex',
    },
  },
});
```

Однако, чтобы позволить этим стилям передавать TypeScript, определения должны быть двусмысленными относительно имен классов CSS и фактических имен свойств CSS. Из-за этих имен классов, которые равны свойствам CSS, следует избегать.

```ts
// ошибка, потому что TypeScript считает, что `@media (min-width: 960px)` является именем класса
// и `content` является свойством css
const ambiguousStyles = createStyles ({
  content: {
    minHeight: '100vh',
  },
  '@media (min -width: 960px) ': {
    content: {
      display: 'flex',
    },
  },
});

// работает просто отлично
const ambiguousStyles = createStyles ({
  contentClass: {
    minHeight: '100vh',
  },
  '@media (min-width: 960px)': {
    contentClass: {
      display: 'flex',
    },
  },
});
```

### Увеличение ваших реквизитов с помощью `WithStyles`

Так как компонент, украшенный `сStyles (styles)` получает специальные `класса, в которые вводится` prop, вам нужно будет определить его реквизиты соответственно:

```ts
const styles = (theme: Theme) => createStyles ({
  root: {/ * ... * /},
  paper: {/ * ... * /},
  : {/ * ... * /},
});

реквизит {
  // нестрочные реквизиты
  foo: number;
  бар: boolean;
  // вложенный стиль реквизита
  классов: {
    root: string;
    бумага: строка;
    кнопка: строка;
  };
}
```

Однако это не очень [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) потому что он требует, чтобы вы поддерживали имена классов (`'root'`, `'paper'`, `'button'`, ...) в двух разных местах. Мы предоставляем оператор типа `WithStyles` чтобы помочь с этим, чтобы вы могли просто написать

```ts
import { WithStyles, createStyles } из '@ material-ui / core';

const styles = (theme: Theme) => createStyles ({
  root: {/ * ... * /},
  paper: {/ * ... * /},
  : {/ * ... * /},
});

Props расширяет WithStyles<typeof styles> {
  foo: number;
  бар: boolean;
}
```

### Украшение компонентов

Применение `withStyles (styles)` как функция работает как ожидалось:

```tsx
const DecoratedSFC = withStyles (стили) (({текст, тип, цвет, классы}: реквизит) => (
  <Typography variant={type} color={color} classes={classes}>
    {text}
  </Typography>
));

const DecoratedClass = withStyles (стили) (
  класс расширяет React.Component<Props> {
    render () {
      const {текст, тип, цвет, классы} = this.props
      return (
        <Typography variant={type} color={color} classes={classes}>
          {text}
        </Typography>
      );
    }
  }
);
```

К сожалению, из-за ограничения тока [декодеров TypeScript](https://github.com/Microsoft/TypeScript/issues/4881), `withStyles (styles)` не могут использоваться в качестве декоратора в TypeScript.

## Настройка `Темы`

При добавлении пользовательских свойств к `Тема`, вы можете продолжать использовать его в строго типизированных образом за счет использования [модуля машинопись в увеличение](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation).

В следующем примере добавлено свойство `appDrawer` , которое объединено с экспортированным `материалом-ui`:

```ts
import { Theme } из '@ material-ui / core / styles / createMuiTheme';
import { Breakpoint } из '@ material-ui / core / styles / createBreakpoints';

объявить модуль '@ material-ui / core / styles / createMuiTheme' {
  interface Theme {
    appDrawer: {
      width: React.CSSProperties ['width']
      точка останова: точка останова
    }
  }
  // разрешить настройку с помощью ` createMuiTheme`
  ThemeOptions {
    appDrawer ?: {
      width ?: React.CSSProperties ['width']
      точка останова ?: точка останова
    }
  }
}
```

И фабрика настраиваемых тем с дополнительными опциями по умолчанию:

**./styles/createMyTheme**:

```ts
import createMuiTheme, { ThemeOptions } из '@ material-ui / core / styles / createMuiTheme';

экспорт функции по умолчанию createMyTheme (options: ThemeOptions) {
  return createMuiTheme ({
    appDrawer: {
      width: 225,
      breakpoint: 'lg',
    },
    ... options,
  })
}
```

Это можно использовать как:

```ts
import createMyTheme из './styles/createMyTheme';

const theme = createMyTheme ({appDrawer: { breakpoint: 'md' }});
```