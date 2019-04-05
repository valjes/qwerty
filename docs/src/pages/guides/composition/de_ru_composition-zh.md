# Состав

<p class="description">Material-UI пытается сделать композицию как можно проще.</p>

## Упаковочные компоненты

Чтобы обеспечить максимальную гибкость и производительность, нам нужен способ узнать природу дочерних элементов, получаемых компонентом. Чтобы решить эту проблему, мы помечаем некоторые из наших компонентов при необходимости с статическим свойством `muiName`.

Тем не менее, пользователям нравится обернуть компоненты, чтобы их улучшить. Это может противоречить нашему решению `muiName`. Если вы столкнулись с этой проблемой, вам необходимо:

1. Переслать свойства.
2. Используйте те же теги для вашего компонента упаковки, который используется с обернутым компонентом.

Давайте посмотрим пример:

```jsx
const WrappedIcon = props => <Icon {...props} />;
WrappedIcon.muiName = 'Icon';
```

{{"demo": "pages / guide / composition / Composition.js"}}

## Свойство компонента

Material-UI позволяет вам изменить корневой узел, который будет отображаться через свойство, называемое `компонентом`. Компонент будет выглядеть следующим образом:

```js
return React.createElement (this.props.component, реквизит)
```

Например, по умолчанию `List` будет отображать элемент `<ul>`. Это можно изменить, передав компонент [React](https://reactjs.org/docs/components-and-props.html#functional-and-class-components) в свойство `компонента`. Следующий пример будет отображать компонент `List` элементом `<nav>` качестве корневого узла:

```jsx
<List component="nav">
  <ListItem>
    <ListItemText primary="Trash" />
  </ListItem>
  <ListItem>
    <ListItemText primary="Spam" />
  </ListItem>
</List>
```

Этот шаблон очень эффективен и обеспечивает большую гибкость, а также способ взаимодействия с другими библиотеками, такими как `-agent-router` или ваша библиотека избранных форм. Но это также **поставляется с небольшим предостережением!**

### Предостережение с инкрустацией

Использование встроенной функции в качестве аргумента для свойства `компонента` может привести к **му неожиданному отключению**, поскольку каждый раз, когда React Renders передает новый компонент в свойство `компонента` передает новый компонент. Например, если вы хотите создать пользовательский список `ListItem` который действует как ссылка, вы можете сделать следующее:

```jsx
const ListItemLink = ({icon, primary, secondary, to}) => (
  <li>
    <ListItem button component={props => <Link to={to} {...props} />}>
      {icon && <ListItemIcon>{icon}</ListItemIcon>}
      <ListItemText inset primary={primary} secondary={secondary} />
    </ListItem>
  </li>
);
```

Однако, поскольку мы используем функцию инлайн изменить обработанный компонент, React размонтирует по ссылке каждый раз , когда `ListItemLink` визуализируются. Мало того, что React обновит DOM без необходимости, эффект пульсации `ListItem` также будет работать неправильно.

Решение простое: **избегать встроенных функций и передать статический компонент в `компонент` собственности** вместо этого. Давайте изменим наш `ListItemLink` на следующее:

```jsx
class ListItemLink расширяет React.Component {
  renderLink = itemProps => <Link to={this.props.to} {...itemProps} />;

  render () {
    const {icon, primary, secondary, to} = this.props;
    возвращение (
      <li>
        <ListItem button component={this.renderLink}>
          {icon && <ListItemIcon>{icon}</ListItemIcon>}
          <ListItemText inset primary={primary} secondary={secondary} />
        </ListItem>
      </li>
    );
  }
}
```

`renderLink` теперь всегда ссылается на один и тот же компонент.

### React Router

Вот демонстрация с [React Router](https://github.com/ReactTraining/react-router):

{{"demo": "pages / guides / composition / ComponentProperty.js"}}