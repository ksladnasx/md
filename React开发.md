# React开发

## JXS

### 概述简介

JXS利用括号将html元素包裹，然后返回，注意最外层包裹只能有一个元素

```jsx
const JSX = (
  <div>
    <h2>Welcome to React!</h2> <br />
    <p>Be sure to close all tags!</p>
    <hr />
  </div>
);
```

与js的区别在于驼峰命名的方式，例如onclick() 变成了onClick(),而类名也变成了className

同时对于自闭合标签，js利用<hr />的写法，而不是<hr>，并且每个标签必须闭合。 例如，为了通过编译换行标签必须始终编写为 `<br />`。 另一方面 `<div>` 可以写成 `<div />` 或者 `<div></div>`。 不同之处在于，在第一个语法版本中，无法在 `<div />` 中包含任何内容。 在后面的挑战中你会发现，这种语法在渲染 React 组件时非常有用。

后面可以用render来将JSX写的阿皮api进行渲染

### 创建函数组件

组件是 React 的核心。 React 中的所有内容都是一个组件，在这里将学习如何创建一个组件。

有两种方法可以创建 React 组件。 第一种方法是使用 JavaScript 函数。 以这种方式定义组件会创建*无状态函数组件*。 将在以后的挑战中介绍应用程序中状态的概念。 目前为止，可以将无状态组件视为能接收数据并对其进行渲染，但不管理或跟踪该数据的更改的组件。 (我们将下一个挑战使用中第二种方式创建 React 组件。)

要用函数创建组件，只需编写一个返回 JSX 或 `null` 的 JavaScript 函数。 需要注意的一点是，React 要求你的函数名以大写字母开头。 下面是一个无状态功能组件的示例，该组件在 JSX 中分配一个 HTML 的 class：

```jsx
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

翻译完成后， `<div>` 将有一个 `customClass` 的 CSS class。

因为 JSX 组件代表 HTML，所以你可以将几个组件放在一起以创建更复杂的 HTML 页面。 这是 React 提供的组件架构的关键优势之一。 它允许用许多独立的组件组合成 UI。 这使得构建和维护复杂的用户界面变得更加容易。

### 创建一个 React 组件

定义 React 组件的另一种方法是使用 ES6 的 `class`语法。 在以下示例中，`Kitten` 扩展了`React.Component`：

```jsx
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

这将创建一个 ES6 类 `Kitten`，它扩展了 `React.Component` 类。 因此，`Kitten` 类现在可以访问许多有用的 React 功能，例如本地状态和生命周期钩子。 如果还不熟悉这些术语，请不要担心，在以后的挑战中我们将更详细地介绍它们。 另请注意，`Kitten` 类中定义了一个调用 `super()` 方法的 `constructor`。 它使用 `super()` 调用父类的构造函数，即本例中的 `React.Component`。 构造函数是使用 `class` 关键字创建的特殊方法，它在实例初始化之前调用。 最佳做法是在组件的 `constructor` 里调用 `super`，并将 `props` 传递给它们， 这样可以保证组件能够正确地初始化。 目前为止 ，需要知道这些代码是必要的。 很快会了解到到构造函数的其他用途以及 `props`。