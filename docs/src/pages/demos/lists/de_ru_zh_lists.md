---
title: Список компонентов React
components: Свернуть, Divider, List, ListItem, ListItemAvatar, ListItemIcon, ListItemSecondaryAction, ListItemText, ListSubheader
---
# Списки

<p class="description">Списки являются непрерывными, вертикальными индексами текста или изображений.</p>

[Списки](https://material.io/design/components/lists.html) представляют собой сплошную группу текста или изображений. Они состоят из элементов, содержащих первичные и дополнительные действия, которые представлены значками и текстом.

## Простой список

{{"demo": "pages / demos / lists / SimpleList.js"}}

Последний элемент предыдущей демонстрации показывает, как вы можете отобразить ссылку:

```jsx
функция ListItemLink (реквизит) {
  return <ListItem button component="a" {...props} />;
}

// ...

<ListItemLink href="#simple-list">
  <ListItemText primary="Spam" />
</ListItemLink>
```

Вы можете найти [демку с React маршрутизатора после этого раздела](/guides/composition/#react-router) документации.

## Список папок

{{"demo": "pages / demos / lists / FolderList.js"}}

## Список вставки

{{"demo": "pages / demos / lists / InsetList.js"}}

## Вложенный список

{{"demo": "pages / demos / lists / NestedList.js"}}

## Выбранный ListItem

{{"demo": "pages / demos / lists / SelectedListItem.js"}}

## Список закрепленных подзаголовков

При прокрутке подзаголовки остаются прикрепленными к верхней части экрана до тех пор, пока они не будут выведены из экрана следующим подзаголовком.

Эта функция опирается на липкое позиционирование CSS. К сожалению , это [не реализовано](https://caniuse.com/#search=sticky) всех браузеры мы поддерживаем. По умолчанию `disableSticky` не поддерживается.

{{"demo": "pages / demos / lists / PinnedSubheaderList.js"}}

## Элементы управления списком

### флажок

Флажок может быть либо основным действием, либо вторичным действием.

Флажок - это основное действие и индикатор состояния для элемента списка. Кнопка комментария - это вторичное действие и отдельная цель.

{{"demo": "pages / demos / lists / CheckboxList.js"}}

Флажок - это вторичное действие для элемента списка и отдельной цели.

{{"demo": "pages / demos / lists / CheckboxListSecondary.js"}}

### переключатель

Переключатель - это вторичное действие и отдельная цель.

{{"demo": "pages / demos / lists / SwitchListSecondary.js"}}

## интерактивный

Ниже приведена интерактивная демонстрация, позволяющая исследовать визуальные результаты различных настроек:

{{"demo": "pages / demos / lists / InteractiveList.js"}}