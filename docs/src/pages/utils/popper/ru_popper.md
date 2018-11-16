---
title: Компонент Поппера
components: огнестрельное оружие
---
# огнестрельное оружие

<p class="description">Поппер может использоваться для отображения некоторого контента поверх другого. Это альтернатива реакционному попперу.</p>

Что нужно знать при использовании компонента `Popper`:

- Попперы полагаются на стороннюю библиотеку [Popper.js](https://github.com/FezVrasta/popper.js) для позиционирования.
- Дети - это [`Portal`](/utils/portal/) чтобы избежать проблем. Вы можете отключить это поведение с помощью `disablePortal`.
- Прокрутка и щелчок не блокируются, как с помощью компонента [`Popover`](/utils/popover/). Размещение popper обновляется с доступной областью в окне просмотра.
- `anchorEl` передается в качестве эталонного объекта для создания нового экземпляра `Popper.js`.

## Простой Поппер

{{"demo": "pages / utils / popper / SimplePopper.js"}}

## Прогулка по детской площадке

{{"demo": "pages / utils / popper / ScrollPlayground.js"}}

## Позиционированный Поппер

{{"demo": "pages / utils / popper / PositionedPopper.js"}}

## Без перехода Popper

{{"demo": "pages / utils / popper / NoTransitionPopper.js"}}

## Поддельный ссылочный объект

Свойство `anchorEl` может быть ссылкой на поддельный элемент DOM. Вам просто нужно создать объект, подобный [`ReferenceObject`](https://github.com/FezVrasta/popper.js/blob/0642ce0ddeffe3c7c033a412d4d60ce7ec8193c3/packages/popper/index.d.ts#L118-L123).

Выделите часть текста, чтобы увидеть поппера:

{{"demo": "pages / utils / popper / FakedReferencePopper.js"}}

## Рендеринг реквизита

Это [реквизит реквизита](https://reactjs.org/docs/render-props.html) демо, что отслеживает локальное состояние для одного поппера.

{{"demo": "pages / utils / popper / RenderPropsPopper.js"}}