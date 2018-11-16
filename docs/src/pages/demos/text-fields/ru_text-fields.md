---
title: Компонент текстового поля
components: FilledInput, FormControl, FormHelperText, Input, InputAdornment, InputBase, InputLabel, OutlinedInput, TextField
---
# Текстовые поля

<p class="description">Текстовые поля позволяют пользователям вводить и редактировать текст.</p>

[Текстовые поля](https://material.io/design/components/text-fields.html) позволяют пользователям вводить текст в пользовательский интерфейс. Они обычно появляются в формах и диалогах.

## Текстовое поле

Компонент оболочки TextField</code> `- это полный контроль формы, включая метку, ввод и текст справки.</p>

<p>{{"demo": "pages / demos / text-fields / TextFields.js"}}</p>

<h2>Изложенные</h2>

<p><code>TextField` поддерживает очерченный стиль.

{{"demo": "pages / demos / text-fields / OutlinedTextFields.js"}}

## заполненный

`TextField` поддерживает заполненный стиль.

{{"demo": "pages / demos / text-fields / FilledTextFields.js"}}

## Компоненты

`TextField` состоит из меньших компонентов ( [`FormControl`](/api/form-control/), [`Вход`](/api/input/), [`Заполненный вход`](/api/filled-input/), [`InputLabel`](/api/input-label/), [`OutlinedInput`](/api/outlined-input/), и [`FormHelperText`](/api/form-helper-text/) ), которые вы можете использовать непосредственно для значительного изменения ваших входных данных формы.

Возможно, вы также заметили, что некоторые некоторые исходные свойства HTML отсутствуют в компоненте TextField</code> `.
Это специально.
Компонент позаботится о наиболее часто используемых свойствах, тогда пользователь может использовать базовый компонент, показанный в следующей демонстрации. Тем не менее, вы можете использовать <code>inputProps` (и `InputProps`, `InputLabelProps` свойств), если вы хотите избежать некоторых шаблонов.

{{"demo": "pages / demos / text-fields / ComposedTextField.js"}}

## входные

{{"demo": "pages / demos / text-fields / Inputs.js"}}

## раскладка

`TextField`, `FormControl` позволяет специфицировать `поля` для изменения вертикального расстояния между входами. Использование `none` (по умолчанию) не будет применять поля к `FormControl`, тогда как `плотных` и `нормальных` будут также заменять других стилей для соответствия спецификации.

{{"demo": "pages / demos / text-fields / TextFieldMargins.js"}}

## Входные украшения

`Ввод` позволяет предоставить `InputAdornment`. Они могут использоваться для добавления префикса, суффикса или действия для ввода. Например, вы можете использовать кнопку значка, чтобы скрыть или открыть пароль.

{{"demo": "pages / demos / text-fields / InputAdornments.js"}}

## Заполненные входные украшения

{{"demo": "pages / demos / text-fields / FilledInputAdornments.js"}}

## Очерченные входные украшения

{{"demo": "pages / demos / text-fields / OutlinedInputAdornments.js"}}

## Отформатированные входы

Вы можете использовать сторонние библиотеки для форматирования ввода. Вы должны обеспечить пользовательскую реализацию элемента `<input>` с помощью свойства `inputComponent`.

Следующий пример использует в [реагирующие-текст-маска](https://github.com/text-mask/text-mask) и [вступают в реакцию номер формата](https://github.com/s-yadav/react-number-format) библиотеки.

{{"demo": "pages / demos / text-fields / FormattedInputs.js"}}

## Индивидуальные входы

Если вы читаете страницу переопределения [стр.](/customization/overrides/) но вы не уверены, что хотите прыгать, вот пример того, как вы можете изменить основной цвет ввода.

{{"demo": "pages / demos / text-fields / CustomizedInputs.js"}}

## С иконкой

Значки могут быть указаны как добавленные или добавленные.

{{"demo": "pages / demos / text-fields / InputWithIcon.js"}}

## Ограничения

Входное обозначение «сжатие» не всегда корректно. Предполагается, что входная метка будет уменьшаться, как только на дисплее появится что-то. В некоторых случаях мы не можем определить состояние «усадки» (ввод количества, входной сигнал даты и времени, ввод полосы). Вы можете заметить перекрытие.

![сокращаться](/static/images/text-fields/shrink.png)

Чтобы решить проблему, вы можете принудительно «сжимать» состояние метки.

```jsx
<TextField InputLabelProps={{ shrink: true }} />
```

или же

```jsx
<InputLabel shrink>Количество</InputLabel>
```