---
title: Компонент Popover React
components: Растет, Поповер
---
# Трещать

<p class="description">Popover можно использовать для отображения некоторого контента поверх другого.</p>

Что нужно знать при использовании компонента `Popover` : - Компонент построен поверх [`Modal`](/utils/modal/). - Прокрутка и щелчок блокируются в отличие от компонента [`Popper`](/utils/popper/).

## Простой Popover

{{"demo": "pages / utils / popover / SimplePopover.js"}}

## Якорная площадка

Используйте переключатели, чтобы отрегулировать позиции `anchorOrigin` и `transformOrigin`. Вы также можете установить `anchorReference от` до `anchorPosition` или `anchorEl`. Когда он равен `anchorPosition`, компонент будет вместо `anchorEl`ссылаться на `anchorPosition` prop, которые вы можете настроить, чтобы установить положение popover.

{{"demo": "pages / utils / popover / AnchorPlayground.js"}}

## Мышь над взаимодействием

Мы демонстрируем, как использовать компонент `Popover` для реализации поведения popover на основе мыши над событием.

{{"demo": "pages / utils / popover / MouseOverPopover.js"}}

## Рендеринг реквизита

Это демонстрация реквизита [render](https://reactjs.org/docs/render-props.html) которая отслеживает локальное состояние для одного popover.

{{"demo": "pages / utils / popover / RenderPropsPopover.js"}}