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

## 用组合的方式创建一个 React 组件

现在来看看如何组合多个 React 组件。 想象一下，现在正在构建一个应用程序，并创建了三个组件：`Navbar`、`Dashboard` 和 `Footer`。

要将这些组件组合在一起，可以创建一个 `App` *父组件*，将这三个组件分别渲染成为*子组件*。 要在 React 组件中渲染一个子组件，需要在 JSX 中将组件名称写作自定义的 HTML 标签。 例如，在 `render` 方法中，可以这样编写：

```jsx
return (
 <App>
  <Navbar />
  <Dashboard />
  <Footer />
 </App>
)
```

当 React 遇到一个自定义 HTML 标签引用另一个组件的时（如本例所示，组件名称包含在 `< />` 中），它在自定义标签的位置渲染该组件的标签。 这可以说明 `App` 组件和 `Navbar`、`Dashboard` 以及 `Footer` 之间的父子关系。

用组合的方式创建一个 React 组件

在代码编辑器中，有一个名为 `ChildComponent` 的简单函数组件和一个名为 `ParentComponent` 的 React 组件。 通过在 `ParentComponent` 中渲染 `ChildComponent` 来将两者组合在一起。 确保使用正斜杠关闭 `ChildComponent` 标签。

**Note:** `ChildComponent` is defined with an ES6 arrow function because this is a very common practice when using React.

```jsx
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        { /* 修改这行下面的代码 */ }
        <ChildComponent />
        { /* 修改这行上面的代码 */ }
      </div>
    );
  }
};
```

就是利于自闭和标签将组件嵌套就行，render() {  }里面进行渲染

## 使用 React 渲染嵌套组件

上一个挑战显示了组合两个组件的简单方法，但是有许多不同的方法可以把 React 组件组合在一起。

组件组合是 React 的强大功能之一。 当使用 React 时，应当先用组件的思路考虑清楚用户界面的结构（如上一个挑战中的 App 示例）。 可以将 UI 分解为基本的构建块，这些构建块就是组件。 这样做有助于将负责 UI 的代码与负责处理应用程序逻辑的代码分开， 并可以大大简化复杂项目的开发和维护。

使用 React 渲染嵌套组件

代码编辑器中定义了两个功能组件，分别是 `TypesOfFruit` 和 `Fruits`。 请用组合或者*嵌套*把 `TypesOfFruit` 组件放到 `Fruits` 组件中， 然后把 `Fruits` 组件放到 `TypesOfFood` 组件中。 结果应该是子组件嵌套在父组件中，父组件嵌套在它本身的父组件中！

```jsx
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
        <li>Strawberries</li>
        <li>Bananas</li>
      </ul>
    </div>
  );
};

const Fruits = () => {
  return (
    <div>
      { /* 修改这行下面的代码 */ }
        <TypesOfFruit />
      { /* 修改这行上面的代码 */ }
    </div>
  );
};

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        { /* 修改这行下面的代码 */ }
        <Fruits />
        { /* 修改这行上面的代码 */ }
      </div>
    );
  }
};
```

## 组合 React 组件

随着挑战继续，将组合使用更复杂的 React 组件和 JSX，有一点需要注意。 在其它组件中渲染 ES6 风格的类组件和渲染在过去几个挑战中使用的简单组件没有什么不同。 可以在其它组件中渲染 JSX 元素、无状态函数组件和 ES6 类组件。

组合 React 组件

在代码编辑器中，`TypesOfFood` 组件已经渲染了一个名为 `Vegetables` 的组件。 此外，还有上次挑战中的 `Fruits` 组件。

在 `Fruits` 中嵌套两个组件，首先 `NonCitrus`，然后是 `Citrus`， 这两个组件都已经引入。 接下来，将 `Fruits` 类组件嵌套到 `TypesOfFood` 组件中，位于 `h1` 标题元素下方和 `Vegetables` 上方。 结果应该是一系列嵌套的组件，它们使用两种不同的组件类型。

```jsx
class Fruits extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h2>Fruits:</h2>
        { /* 修改这行下面的代码 */ }
          <NonCitrus />
          <Citrus />
        { /* 修改这行上面的代码 */ }
      </div>
    );
  }
};

class TypesOfFood extends React.Component {
  constructor(props) {
     super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        { /* 修改这行下面的代码 */ }
          <Fruits />
        { /* 修改这行上面的代码 */ }
        <Vegetables />
      </div>
    );
  }
};
```

#### 1. **父子关系的体现**

在 React 中，父子关系是通过组件的嵌套来体现的。具体来说：

- **`TypesOfFood` 是父组件**：因为它在自己的 `render` 方法中调用了 `Fruits` 和 `Vegetables` 组件。

  jsx复制

  ```jsx
  <Fruits />
  <Vegetables />
  ```

  这里的 `<Fruits />` 表示 `TypesOfFood` 组件将 `Fruits` 组件作为子组件嵌套在自己内部。

- **`Fruits` 是子组件**：因为它被 `TypesOfFood` 组件调用，并且它自身也嵌套了 `NonCitrus` 和 `Citrus` 组件。

  jsx复制

  ```jsx
  <NonCitrus />
  <Citrus />
  ```

#### 2. **为什么删除 `TypesOfFood` 后 `Fruits` 无法单独渲染？**

在 React 中，组件的渲染是从根组件开始的。根组件通常是通过 `ReactDOM.render` 或类似的方法挂载到 DOM 上的。例如：

jsx复制

```jsx
ReactDOM.render(<TypesOfFood />, document.getElementById('root'));
```

- **`TypesOfFood` 是根组件**：当 `TypesOfFood` 被挂载时，它会按照自己的 `render` 方法中的定义，依次渲染 `Fruits` 和 `Vegetables`。
- **`Fruits` 是子组件**：它依赖于父组件 `TypesOfFood` 来被渲染。

如果你删除了 `TypesOfFood`，那么 `Fruits` 就失去了被挂载的入口点。React 不会自动渲染 `Fruits`，因为没有一个明确的调用链来告诉 React 从哪里开始渲染。

### 如何单独渲染 `Fruits`？

如果你希望单独渲染 `Fruits`，你需要直接在根组件中调用它，而不是通过 `TypesOfFood`。例如：

jsx复制

```jsx
ReactDOM.render(<Fruits />, document.getElementById('root'));
```

这样，`Fruits` 就会作为根组件被渲染，而不需要依赖于 `TypesOfFood`。

### 总结

- **父子关系**：通过组件的嵌套来体现。父组件在其 `render` 方法中调用子组件。
- **渲染机制**：React 的渲染是从根组件开始的。如果父组件被删除，子组件无法被自动渲染，因为没有入口点。
- **单独渲染子组件**：可以通过直接在根组件中调用子组件来实现。

## 将 class 组件渲染到 DOM 树

还记不记得在之前的挑战中使用 ReactDOM API 将 JSX 元素渲染到 DOM， 这与渲染 React 组件的过程十分相似。 过去的几个挑战主要针对组件和组合，因此渲染是在幕后完成的。 但是，如果不调用 ReactDOM API，编写的任何 React 代码都不会渲染到 DOM。

复习一下语法： `ReactDOM.render(componentToRender, targetNode)`。 第一个参数是要渲染的 React 组件。 第二个参数是要在其中渲染该组件的 DOM 节点。

传递到`ReactDOM.render()` 的React 组件与 JSX 元素略有不同。 对于 JSX 元素，传入的是要渲染的元素的名称。 但是，对于 React 组件，需要使用与渲染嵌套组件相同的语法，例如`ReactDOM.render(<ComponentToRender />, targetNode)`。 此语法用于 ES6 class 组件和函数组件都可以。

将 class 组件渲染到 DOM 树

在后台引入了 `Fruits` 和 `Vegetables` 组件。 将两个组件渲染为 `TypesOfFood` 组件的子组件，然后将 `TypesOfFood` 渲染到 DOM 节点， 在这个挑战中，请渲染到 `id='challenge-node'`的 `div` 中。

```jsx
class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        {/* 修改这行下面的代码 */}
        <Fruits />
        <Vegetables />
        {/* 修改这行上面的代码 */}
      </div>
    );
  }
};

// 修改这行下面的代码
 ReactDOM.render(<TypesOfFood />,document.getElementById('challenge-node'))
```

## 将 Props 传递给无状态函数组件

之前的挑战涵盖了关于在 React 中创建和组合 JSX 元素、函数组件和 ES6 风格的类组件的很多内容。 有了这个基础，现在是时候看看 React 中的另一个常见特性 **props** 了。 在 React 中，可以将属性传递给子组件。 假设有一个 `App` 组件，该组件渲染了一个名为 `Welcome` 的子组件，它是一个无状态函数组件。 可以通过以下方式给 `Welcome` 传递一个 `user` 属性：

```jsx
<App>
  <Welcome user='Mark' />
</App>
```

可以把创建的 React 支持的**自定义 HTML 属性**传递给组件。 在上面的例子里，将创建的属性 `user` 传递给组件 `Welcome`。 由于 `Welcome` 是一个无状态函数组件，它可以像这样访问该值：

```jsx
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```

调用 `props` 这个值是常见做法，当处理无状态函数组件时，基本上可以将其视为返回 JSX 的函数的参数。 这样，你就可以在函数体中访问该值。 但对于类组件，访问方式会略有不同。

将 Props 传递给无状态函数组件

代码编辑器中有 `Calendar` 和 `CurrentDate` 组件。 从 `Calendar` 组件渲染 `CurrentDate` 时，从 JavaScript 的 `Date` 对象分配当前日期，并将其作为 `date` 属性传入。 然后访问 `CurrentDate` 组件的 `prop`，并在 `p` 标签中显示其值。 请注意，要将 `prop` 的值视为 JavaScript，必须将它们括在花括号中，例如`date={Date()}`。

```jsx
const CurrentDate = (props) => {
  return (
    <div>
      { /* 修改这行下面的代码 */ }
      <p>The current date is: {props.date}</p>
      { /* 修改这行上面的代码 */ }
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    {/* 将 currentDate 作为 date 属性传递给 CurrentDate 组件 */}
        const currentDate = new Date().toLocaleDateString(); 
    return (
      <div>
        <h3>What date is it?</h3>
        { /* 修改这行下面的代码 */ }
        <CurrentDate date={currentDate} />
        { /* 修改这行上面的代码 */ }
      </div>
    );
  }
};
```

注意获取当前时间的方式：

直接Date()调用：

```jsx
<CurrentDate date={Date()} />
```

利于Date对象调用：

```jsx
<CurrentDate date={Date().toLocaleDateString();} />
```

## 数组传参

上一个挑战演示了如何将来自父组件的信息作为 `props` 传递给子组件。 这个挑战着眼于如何将数组作为 `props` 传递。 要将数组传递给 JSX 元素，必须将其视为 JavaScript 并用花括号括起来。

```jsx
<ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

这样，子组件就可以访问数组属性 `colors`。 访问属性时可以使用 `join()` 等数组方法。

```jsx
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```

This will join all `colors` array items into a comma separated string and produce: `<p>green, blue, red</p>`. Later, we will learn about other common methods to render arrays of data in React.

传递一个数组作为 Props

There are `List` and `ToDo` components in the code editor. When rendering each `List` from the `ToDo` component, pass in a `tasks` property assigned to an array of to-do tasks, for example `["walk dog", "workout"]`. Then access this `tasks` array in the `List` component, showing its value within the `p` element. Use `join(", ")` to display the `props.tasks` array in the `p` element as a comma-separated list. Today's list should have at least 2 tasks and tomorrow's should have at least 3 tasks.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

// 定义 List 组件
const List = (props) => {
  // 使用 join(", ") 将 tasks 数组转换为逗号分隔的字符串
  const tasksString = props.tasks.join(", ");
  return <p>{tasksString}</p>;
};

// 定义 ToDo 组件
class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        {/* 传递 tasks 属性给第一个 List 组件 */}
        <List tasks={['walk dog', 'workout']} />
        <h2>Tomorrow</h2>
        {/* 传递 tasks 属性给第二个 List 组件 */}
        <List tasks={['walk dog', 'workout', 'clean room']} />
      </div>
    );
  }
};

// 渲染 ToDo 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<ToDo />, document.getElementById('challenge-node'));
```

同时对于数组每个元素也可用map来渲染List 组件需要将 tasks 属性中的每个任务渲染到一个 <p> 标签中。以下是修改后的代码，确保 List 组件正确渲染 tasks 属性中的每个任务：

```jsx

import React from 'react';
import ReactDOM from 'react-dom';

// 定义 List 组件
const List = (props) => {
  // 使用 map 方法渲染 tasks 数组中的每个任务
  return (
    <div>
      {props.tasks.map((task, index) => (
        <p key={index}>{task}</p>
      ))}
    </div>
  );
};
```

## 使用默认的 Props

`ShoppingCart` 组件应该有一个 `{ items: 0 }` 的默认 prop。

React 还有一个设置默认 props 的选项。 可以将默认 props 作为组件本身的属性分配给组件，React 会在必要时分配默认 prop。 如果没有显式的提供任何值，这允许指定 prop 值应该是什么。 例如，如果声明 `MyComponent.defaultProps = { location: 'San Francisco' }`，即定义一个 location 属性，并且其值在没有另行制定的情况下被设置为字符串 `San Francisco`。 如果 props 未定义，则 React 会分配默认 props，但如果你将 `null` 作为 prop 的值，它将保持 `null`。

```jsx
const ShoppingCart = (props) => {
  return (
    <div>
      <h1>Shopping Cart Component</h1>
    </div>
  )
};
// 修改这行下面的代码
ShoppingCart.defaultProps = { items: 0 }
```

## 覆盖默认的 Props

在 React 中，设置默认的 props 是一个很有用的特性， 显式设置组件的 prop 值即可覆盖默认 props。

覆盖默认的 Props

`ShoppingCart` 组件现在渲染了一个子组件 `Items`。 该 `Items` 组件有一个默认 `quantity` prop，其值被设置为整数 `0`。 通过传入数值 `10` 来覆盖 `quantity` 的默认 prop。

**注意：** 请记住，向组件添加 prop 的语法与添加 HTML 属性类似。 **但是，由于 `quantity` 的值是整数，所以它不会加引号，但应该用花括号括起来，** 例如`{100}`。 这个语法告诉 JSX 直接将花括号中的值解释为 JavaScript。

## 使用 PropTypes 来定义 Props 的类型

React 提供了有用的类型检查特性，以验证组件是否接收了正确类型的 props。 例如，应用程序调用 API 来检索数据是否是数组，然后将数据作为 prop 传递给组件。 可以在组件上设置 `propTypes`，以要求数据的类型为 `array`。 当数据是任何其它类型时，都会抛出警告。

当提前知道 prop 的类型时，最佳实践是设置其 `propTypes`。 可以为组件定义 `propTypes` 属性，方法与定义 `defaultProps` 相同。 这样做将检查一个键的 prop 是否是给定类型。 这里有一个示例，表示名为 `handleClick` 的 prop 应为 `function` 类型：

```js
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```

在上面的示例中，`PropTypes.func` 部分检查 `handleClick` 是否为函数。 添加 `isRequired`，告诉 React `handleClick` 是该组件的必需属性。 如果没有那个属性，将出现警告。 还要注意 `func` 代表 `function` 。 在 7 种 JavaScript 原始类型中，`function` 和 `boolean`（写为 `bool` ）是唯一使用异常拼写的两种类型。 除了原始类型，还有其他类型可用。 例如，你可以检查 prop 是否为 React 元素。 请查看[文档](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)以获取所有选项。

**注意：**在 React v15.5.0 中, `PropTypes` 可以从 React 中单独引入，例如：`import PropTypes from 'prop-types';`。

使用 PropTypes 来定义 Props 的类型

为 `Items` 组件定义 `propTypes`，以要求 `quantity` 作为 prop，并验证它是否为 `number` 类型。

```jsx
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};

// 修改这行下面的代码
Items.propTypes = {quantity: PropTypes.number.isRequired }
// 修改这行上面的代码

Items.defaultProps = {
  quantity: 0
};

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items />
  }
};
```

## 使用 this.props 访问 Props

前几项挑战涵盖了将 props 传递给子组件的基本方法。 但是，倘若接收 prop 的子组件不是无状态函数组件，而是一个 ES6 类组件，又当如何呢？ ES6 类组件访问 props 的方法略有不同。

任何时候，如果要引用类组件本身，可以使用 `this` 关键字。 要访问类组件中的 props，需要在在访问它的代码前面添加 `this`。 例如，如果 ES6 类组件有一个名为 `data` 的 prop，可以在 JSX 中这样写：`{this.props.data}`。

使用 this.props 访问 Props

在父组件 `App` 中渲染 `Welcome` 组件的一个实例。 在这里，给 `Welcome` 一个 `name` 的 prop，并给它赋值一个字符串。 在 `Welcome` 的子节点里，访问 `strong` 标签内的 `name` prop。

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
            { /* 修改这行下面的代码 */ }
            <Welcome name="hei" />
            { /* 修改这行上面的代码 */ }
        </div>
    );
  }
};

class Welcome extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
          { /* 修改这行下面的代码，这里就直接调用参数了 */ }
          <p>Hello, <strong>{this.props.name}</strong>!</p>
          { /* 修改这行上面的代码 */ }
        </div>
    );
  }
};
```

## 复习

在代码编辑器中有一个 `CampSite` 组件，它把 `Camper` 组件渲染为自己的子组件。 定义 `Camper` 组件，并为其分配默认 props `{ name: 'CamperBot' }`。 可以在 `Camper` 组件内部渲染任何你想要的代码，但是要确保有一个 `p` 元素，它只包含作为 `prop` 传递的 `name` 值。 最后，在 `Camper` 组件上定义 `propTypes`，要求提供 `name` 作为 prop，并验证它是 `string` 类型。

```jsx
class CampSite extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <Camper/>
      </div>
    );
  }
};
// 修改这行下面的代码

// 定义 Camper 组件
const Camper = (props) => {
  return (
    <div>
      <p>{props.name}</p>
    </div>
  );
};

// 定义默认的 props
Camper.defaultProps = {
  name: 'CamperBot'
};

// 定义 propTypes
Camper.propTypes = {
  name: PropTypes.string.isRequired
};
```

## 创建一个有状态的组件

React 中最重要的主题之一是 `state`。 state 包含应用程序需要了解的任何数据，这些数据可能会随时间而变化。 应用程序能够响应 state 的变更，并在必要时显示更新后的 UI。 React 为现代 Web 应用程序的状态管理提供了一个很好的解决方案。

可以在类组件的 `constructor` 上声明 `state` 属性来在 React 组件中创建 state， 它在创建时使用 `state` 初始化组件。 `state` 属性必须设置为 JavaScript `object`（对象）。 声明如下：

```jsx
this.state = {

}
```

可以在组件的整个生命周期内访问 `state` 对象， 可以更新它、在 UI 中渲染它，也可以将其作为 props 传递给子组件。 `state` 对象的使用可以很简单，亦可以很复杂，就看你怎么用了。 请注意，必须通过扩展 `React.Component` 来创建类组件，以便像这样创建 `state`。

创建一个有状态的组件

在代码编辑器里，有一个组件尝试渲染 `state` 中的 `firstName` 属性。 但是 `state` 还没有定义。 在 `constructor` 中使用 `state` 初始化这个组件，并将你的名字赋值给 `firstName` 属性。

```jsx
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    // 只修改这一行下面的代码
    this.state = {
      firstName: 'Kimi' // 将你的名字赋值给 firstName
    };
    // 只修改这一行上面的代码
  }
  render() {
    return (
      <div>
        <h1>{this.state.firstName}</h1>
      </div>
    );
  }
};
```

定义了组件的初始 state 之后，就可以在要渲染的 UI 中显示它。 如果组件是有状态的，它将始终可以访问 `render()` 方法中 `state` 的数据。 就可以使用 `this.state` 访问数据。

如果想在 render 方法的 `return` 中访问 state 值，必须把这个值用花括号括起来。

`state` 是 React 组件中最强大的特性之一， 它可以跟踪应用程序中的重要数据，并根据数据的变化渲染 UI。 如果数据发生变化，UI 也会随之改变。 React 使用所谓的虚拟 DOM 来跟踪幕后的变化。 当 state 数据更新时，它会使用该数据触发组件的重新渲染 -- 包括接收 prop 数据的子组件。 React 只在必要的时候更新实际的 DOM， 这意味着你不必担心 DOM 的变更， 只需声明 UI 的外观即可。

注意，如果组件是有状态的，其它组件并不知道它的 `state`。 它的 `state` 是完全封装的，或者是局限于组件本身的，除非你将 state 数据作为 `props` 传递给子组件。 封装 `state` 的概念非常重要，因为它允许编写特定的逻辑，然后将该逻辑包含并隔离在代码中的某个位置。

在用户界面中渲染状态

在代码编辑器中，`MyComponent` 是一个有状态组件， 在组件的 render 方法中定义一个`h1`标签，该方法从组件的 state 渲染 `name` 的值。

**注意：** `h1` 应该只渲染来自 `state` 的值。 在 JSX 中，使用花括号 `{ }` 编写的任何代码都将被视为 JavaScript。 因此，要访问 `state` 中的值，只需将引用括在花括号中即可。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    return (
      <div>
        { /* 修改这行下面的代码 */ }
      <h1>{this.state.name}</h1>
        { /* 修改这行上面的代码 */ }
      </div>
    );
  }
};
```

## 以另一种方式在用户界面中渲染状态

还有另一种方法可以访问组件中的 `state`。 在 `render()` 方法中，在 `return` 语句之前，可以直接编写 JavaScript。 例如，可以声明函数、从 `state` 或 `props` 中访问数据、对此数据执行计算等。 然后，可以将任何数据赋值给 `return` 语句中可以访问的变量。

以另一种方式在用户界面中渲染状态

在 `MyComponent` 的 render 方法中，定义一个名为 `name` 的 `const`（常量），并将其设置为组件 `state` 中的 name 值。 因为可以直接在代码部分编写 JavaScript，所以不需要用大括号括起来。

接下来，在 return 语句中，在 `h1` 标签中渲染变量 `name` 的值。 记住，在 return 语句中需要使用 JSX 语法（用到 JavaScript 的花括号）。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    // 修改这行下面的代码
     const name = this.state.name;
    // 修改这行上面的代码
    return (
     
      <div>
        { /* 修改这行下面的代码 */ }
          {name}
        { /* 修改这行上面的代码 */ }
      </div>
    );
  }
};
```

## 用 this.setState 设置状态

前面的挑战涵盖了组件的 `state` 以及如何在 `constructor` 中初始化 state。 还有一种方法可以更改组件的 `state`。 React 提供了 `setState` 方法来更新组件的 `state`。 在组件类中调用 `setState` 方法如下所示：`this.setState()`，传入键值对的对象， 其中键是 state 属性，值是更新后的 state 数据。 例如，如果我们在 state 中存储 `username`，并想要更新它，代码如下所示：

```jsx
this.setState({
  username: 'Lewis'
});
```

React 要求永远不要直接修改 `state`，而是在 state 发生改变时始终使用 `this.setState()`。 此外，应该注意，React 可以批量处理多个 state 更新以提高性能。 这意味着通过 `setState` 方法进行的 state 更新可以是异步的。 `setState` 方法有一种替代语法可以解决异步问题， 虽然这很少用到，但是最好还是记住它！ 请查阅我们的 [React 文章](https://www.freecodecamp.org/chinese/news/what-is-state-in-react-explained-with-examples/)了解更多详情。

用 this.setState 设置状态

代码编辑器中有一个 `button` 元素，它有一个 `onClick()` handler。 当 `button` 在浏览器中接收到单击事件时触发此 handler，并运行 `MyComponent` 中定义的 `handleClick` 方法。 在 `handleClick` 方法中，使用 `this.setState()` 更新组件的 `state`。 设置 `state` 中的 `name` 属性为字符串 `React Rocks!`。

单击按钮查看渲染的 state 的更新。 如果不完全理解单击处理程序代码在此时的工作方式，请不要担心。 在接下来的挑战中会有讲述。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    // 修改这行下面的代码
    this.setState({
      name:"React Rocks!"
    })
    // 修改这行上面的代码
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

## 将 this 绑定到 Class 方法上

除了设置和更新 `state` 之外，还可以为组件类定义方法。 类方法通常需要使用 `this` 关键字，以便它可以访问方法中类的属性（例如 `state` 和 `props`）。 有几种方法可以让类方法访问 `this`。

一种常见的方法是在构造函数中显式地绑定 `this`，这样当组件初始化时，`this` 就会绑定到类方法。 你可能已经注意到上一个挑战在构造函数中的 `handleClick` 方法使用了 `this.handleClick = this.handleClick.bind(this)`。 然后，当在类方法中调用像 `this.setState()` 这样的函数时，`this` 指的是这个类，而不是 ``。

**注意：** `this`关键字是 JavaScript 中最令人困惑的方面之一，但它在 React 中扮演着重要的角色。 虽然它的行为在这里是完全正常的，但是这些课程并不深入研究`this`，所以如果以上内容令你感到困惑，请参考其他课程！

将 this 绑定到 Class 方法上

代码编辑器有一个带有 `state` 的组件，用于跟踪项目计数。 它还有一个方法，允许设置文本为 `You clicked!`。 但是，该方法不起作用，因为它使用了未定义的 `this` 关键字。 可以通过将 `this` 显式绑定到组件构造函数中的 `handleClick()`方法来修复它。

接下来，向 render 方法中的 `button` 元素添加一个单击处理程序。 当按钮接收到单击事件时，它应该触发 `handleClick()` 方法。 记住，传递给 `onClick` 处理程序的方法需要使用花括号，因为它应该直接被解释为 JavaScript。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      text: "Hello"
    };
this.setState({
   text: "Hello"
});
  }
  handleClick() {
    this.setState({
      text: "You clicked!"
    });
  }
  render() {
    return (
      <div>
        { /* 修改这行下面的代码 */ }
        <button onClick={this.handleClick.bind(this) }>Click Me</button>
        { /* 修改这行上面的代码 */ }
        <h1>{this.state.text}</h1>
      </div>
    );
  }
};
```

完成上述步骤后，可以单击按钮并看到 `You clicked!`。

## 使用 State 切换元素

有时可能在更新状态的时候想知道上一个状态是什么。 但是状态更新是异步的，这意味着 React 可能会把多个 `setState()` 集中在一起批量更新。 所以计算下一个值时 `this.state` 或者 `this.props` 不能作为当前值。 所以最好不要写如下的代码：

```jsx
this.setState({
  counter: this.state.counter + this.props.increment
});
```

正确的做法是，给 `setState` 传入一个函数，这个函数可以访问 state 和 props。 给 `setState` 传入函数可以保证 state 和 props 是正确的值。 代码可以重写为这样：

```jsx
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

如果只需要 `state`，那么用下面没有 `props` 的格式也是可以的：

```jsx
this.setState(state => ({
  counter: state.counter + 1
}));
```

注意一定要把 object 放在括号里，否则 JavaScript 会认为这只是代码片段。

使用 State 切换元素

`MyComponent` 有一个初始值为 `false` 的`visibility` 属性。 如果 `visibility` 的值为 true，render 方法返回一个视图，如果为 false，返回另一个视图。

目前，无法更新组件 `state` 中的 `visibility` 属性， 该值应在 true 和 false 之间来回切换。 按钮上有一个单击处理程序，它触发一个名为 `toggleVisibility()` 的类方法。 给函数传入 `setState` 来定义此方法，以便 `visibility` 的 `state` 在调用方法时切换到相反的值。 如果 `visibility` 是 `false`，则该方法将其设置为`true`，反之亦然。

最后，单击按钮以查看基于其 `state` 的组件的条件渲染。

**提示：** 不要忘记将 `this` 关键字绑定到 `constructor` 中的方法上！

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false // 初始化 state
    };
  }

  // 定义 toggleVisibility 方法
  toggleVisibility() {
    this.setState((state) => ({
      visibility: !state.visibility // 切换 visibility 的值
    }));
  }

  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={() => this.toggleVisibility()}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={() => this.toggleVisibility()}>Click Me</button>
        </div>
      );
    }
  }
};

// 渲染 MyComponent 到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<MyComponent />, document.getElementById('challenge-node'));
```

## 写一个简单的计数器

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0 // 初始化 state
    };
    // 绑定方法
    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
    this.reset = this.reset.bind(this);
  }

  // 定义 increment 方法
  increment() {
    this.setState((state) => ({
      count: state.count + 1
    }));
  }

  // 定义 decrement 方法
  decrement() {
    this.setState((state) => ({
      count: state.count - 1
    }));
  }

  // 定义 reset 方法
  reset() {
    this.setState({
      count: 0
    });
  }

  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};

// 渲染 Counter 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<Counter />, document.getElementById('challenge-node'));
```

注意方法在定义之前要在构造器中绑定好先：

```jsx
 constructor(props) {
    super(props);
    this.state = {
      count: 0 // 初始化 state
    };
    // 绑定方法
    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
    this.reset = this.reset.bind(this);
  }
```

## 创建一个可以控制的输入框

应用程序可能在 `state` 和渲染的 UI 之间有更复杂的交互。 例如，用于文本输入的表单控件元素（如 `input` 和 `textarea`）在用户键入时在 DOM 中维护自己的 state。 通过 React，可以将这种可变 state 转移到 React 组件的 `state` 中。 用户的输入变成了应用程序 `state` 的一部分，因此 React 控制该输入字段的值。 通常，如果 React 组件具有用户可以键入的输入字段，那么它将是一个受控的输入表单。

创建一个可以控制的输入框

代码编辑器具有一个名为 `ControlledInput` 的组件框架，用于创建受控的 `input` 元素。 组件的 `state` 已经被包含空字符串的 `input` 属性初始化。 此值表示用户在 `input` 字段中键入的文本。

首先，创建一个名为 `handleChange()` 的方法，该方法具有一个名为 `event` 的参数。 方法被调用时，它接收一个 `event` 对象，该对象包含一个来自 `input` 元素的字符串文本。 可以使用方法内的 `event.target.value` 来访问这个字符串。 用这个新字符串更新组件的`state`的`input`属性。

在 `render` 方法中的 `h4` 标签之上创建 `input` 元素。 添加一个 `value` 属性，使其等于组件 `state` 的 `input` 属性。 Then add an `onChange` property set to the `handleChange()` event handler method.

在输入框中键入时，文本由 `handleChange()` 方法处理，文本被设置为本地 `state` 中的 `input` 属性，并渲染在页面上的 `input` 框中。 组件 `state` 是输入数据的唯一真实来源。

最后，不要忘记在构造函数中添加必要的绑定。

```jsx
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    // 修改这行下面的代码
 // 绑定 handleChange 方法
    this.handleChange = this.handleChange.bind(this);
    // 修改这行上面的代码
  }
  // 修改这行下面的代码
// 定义 handleChange 方法
  handleChange(event) {
    this.setState({
      input: event.target.value // 更新 state 中的 input 属性
    });
  }
  // 修改这行上面的代码
  render() {
    return (
      <div>
        { /* 修改这行下面的代码 */}
        <input
          type="text"
          value={this.state.input} // 设置 input 的 value 属性
          onChange={this.handleChange} // 设置 input 的 onChange 属性
        />
        { /* 修改这行上面的代码 */}
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```

## 创建一个可以控制的表单

创建一个可以控制的表单

`MyForm` 组件中是一个带有提交处理程序的空 `form` 元素， 提交处理程序将在提交表单时被调用。

我们增加了一个提交表单的按钮。 可以看到它的 `type` 被设置为 `submit`，表明它是控制表单提交的按钮。 在 `form` 中添加 `input` 元素，并像上个挑战一样设置其 `value` 和 `onChange()` 属性。 然后，应该完成 `handleSubmit` 方法，以便将组件 state 属性 `submit` 设置为本地 `state` 下的当前输入值。

**注意：** 还必须在提交处理程序中调用 `event.preventDefault()`，以防止将会刷新网页的默认的表单提交行为。 为了便于学员操作，默认行为在这里被禁用，以防止重置挑战的代码。

最后，在 `form` 元素之后创建一个 `h1` 标签，该标签从组件的 `state` 渲染 `submit` 的值。 然后，可以在表单中键入任何内容，然后单击按钮（或按 enter 键），输入会渲染到页面上。

```jsx
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    // 修改这行下面的代码
    event.preventDefault()
    this.setState({
      submit: this.state.input  //触发后，会将状态中的将submit的值赋值为状态中的input的值
    });
    // 修改这行上面的代码
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          {/* 修改这行下面的代码 */}
          <input
          type="text"
          value={this.state.input} // 设置 input 的 value 属性
          onChange={this.handleChange} // 设置 input 的 onChange 属性
        />
          {/* 修改这行上面的代码 */}
          <button type='submit'  >Submit!</button>
        </form>
        {/* 修改这行下面的代码 */}
        <h1>{this.state.submit}</h1>
        {/* 修改这行上面的代码 */}
      </div>
    );
  }
}
```

## 将 State 作为 Props 传递给子组件

在之前的挑战中，看到了很多将 props 传递给子 JSX 元素和子 React 组件的例子。 你可能想知道那些 props 是从哪里来的。 一个常见的模式是：有状态组件中包含对应用程序很重要的 `state`，然后用它渲染子组件。 如果想让这些组件能够访问该 `state` 的某些部分，就把这些部分作为 props 传入。

例如，有一个 `App` 组件可以渲染 `Navbar` 以及其他组件。 `App` 里的 `state` 包含大量用户信息，但 `Navbar` 只需要访问用户的用户名，以便显示它。 将该 `state` 作为 prop 传递给`Navbar`组件。

这个模式说明了 React 中的一些重要范例。 第一个是*单向数据流*， state 沿着应用程序组件树的一个方向流动，从有状态父组件到子组件， 子组件只接收它们需要的 state 数据。 第二，复杂的有状态应用程序可以分解成几个，或者可能是一个单一的有状态组件。 其余组件只是从父组件简单的接收 state 作为 props，并从该 state 渲染 UI。 它开始创建一种分离，在这种分离中，state 管理在代码的一部分中处理，而 UI 渲染在另一部分中处理。 将 state 逻辑与 UI 逻辑分离是 React 的关键原则之一。 当它被正确使用时，它使得复杂的、有状态的应用程序的设计变得更容易管理。

将 State 作为 Props 传递给子组件

`MyApp` 组件是有状态的，并将 `Navbar` 组件渲染为子组件。 将 `state` 的 `name` 属性向下传递给子组件，然后在 `h1` 中显示该 `name` ，h1 是 `Navbar` render方法的一部分。 `name` 应该显示在文本 `Hello, my name is:` 后面。

```jsx
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         {/* 修改这行下面的代码 */}
         <Navbar name={this.state.name}/>
         {/* 修改这行上面的代码 */}
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      {/* 修改这行下面的代码 */}
      <h1>Hello, my name is: {name}</h1>
      {/* 修改这行上面的代码 */}
    </div>
    );
  }
};
```

## 传递回调作为 Props

可以将 `state` 作为 props 传递给子组件，但不仅限于传递数据。 你也可以将处理函数或在 React 组件中定义的任何方法传递给子组件。 这就是子组件与父组件交互的方式。 可以把方法像普通 prop 一样传递给子组件， 它会被分配一个名字，可以在子组件中的 `this.props` 下访问该方法的名字。

传递回调作为 Props

代码编辑器中列出了三个组件。 `MyApp` 是父组件，`GetInput` 和`RenderInput` 是它将要渲染的子组件。 将 `GetInput` 组件添加到 `MyApp` 的 render 方法，然后将 `MyApp` 的 `state` 中的 `inputValue` 传入名为 `input` 的 prop。 还要创建一个名为 `handleChange` 的 prop，并将输入处理程序 `handleChange` 传递给它。

接下来，将 `RenderInput` 添加到 `MyApp` 中的 render 方法中，然后创建一个名为 `input` 的 prop，并将 `state` 中的 `inputValue` 传递给它。 完成后，可以在 `GetInput` 组件中的 `input` 字段中键入内容，然后该组件通过 props 调用其父组件中的处理函数方法。 这将更新处于父组件 `state` 中的 input，该 input 将作为 props 传递给两个子组件。 观察数据如何在组件之间流动，以及单一数据源如何保持父组件`state`。 诚然，这个示例有点刻意，但是应该能用来说明数据和回调是如何在 React 组件之间传递的

```jsx
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
       {/* 将 GetInput 组件添加到 MyApp 的 render 方法中 */}
        <GetInput 
          input={this.state.inputValue} 
          handleChange={this.handleChange} 
        />
        {/* 将 RenderInput 组件添加到 MyApp 的 render 方法中 */}
        <RenderInput input={this.state.inputValue} />
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```

## 使用生命周期方法：componentDidMount

某些时候，大多数 web 开发人员需要调用 API 接口来获取数据。 如果正在使用 React，知道在哪里执行这个动作是很重要的。

React 的最佳实践是在生命周期方法 `componentDidMount()` 中对服务器进行 API 调用或任何其它调用。 将组件装载到 DOM 后会调用此方法。 此处对 `setState()` 的任何调用都将触发组件的重新渲染。 在此方法中调用 API 并用 API 返回的数据设置 state 时，一旦收到数据，它将自动触发更新。

使用生命周期方法：componentDidMount

`componentDidMount()` 中有一个模拟 API 调用。 它在 2.5 秒后设置 state，以模拟调用服务器检索数据。 本示例请求站点的当前活动用户总数。 在 render 方法中，把 `activeUsers` 渲染到文字 `Active Users:` 后的 `h1` 标签中。 观看预览中发生的事情，随意更改超时时间以查看不同的效果。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        {/* 修改这行下面的代码 */}
        <h1>Active Users: {this.state.activeUsers}</h1>
        {/* 修改这行上面的代码 */}
      </div>
    );
  }
}
```

## 生命周期

React 的生命周期方法是类组件中的一组特殊的方法，它们允许你在组件的生命周期的不同阶段执行代码。这些方法可以分为三个主要阶段：挂载阶段（Mounting）、更新阶段（Updating）和卸载阶段（Unmounting）。

以下是 React 生命周期方法的详细介绍：

### 1. 挂载阶段（Mounting）

挂载阶段是指组件从无到有，被插入到 DOM 中的过程。在这个阶段，组件会依次调用以下方法：

#### 1.1 `constructor(props)`

- **作用**：构造函数是组件生命周期的第一个方法，用于初始化组件的状态（`state`）。

- **调用时机**：组件实例化时。

- **示例**：

  jsx复制

  ```jsx
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
  ```

#### 1.2 `static getDerivedStateFromProps(props, state)`

- **作用**：在组件挂载之前调用，用于根据 `props` 更新 `state`。

- **调用时机**：组件挂载之前，以及每次 `props` 更新时。

- **返回值**：返回一个对象，用于更新 `state`。

- **示例**：

  jsx复制

  ```jsx
  static getDerivedStateFromProps(props, state) {
    if (props.value !== state.value) {
      return { value: props.value };
    }
    return null;
  }
  ```

#### 1.3 `render()`

- **作用**：返回组件的 JSX 结构，用于渲染到 DOM 中。

- **调用时机**：组件挂载时，以及每次 `state` 或 `props` 更新时。

- **示例**：

  jsx复制

  ```jsx
  render() {
    return <div>{this.state.count}</div>;
  }
  ```

#### 1.4 `componentDidMount()`

- **作用**：组件挂载完成后调用，通常用于执行副作用操作，如 API 请求、订阅事件等。

- **调用时机**：组件挂载完成后。

- **示例**：

  jsx复制

  ```jsx
  componentDidMount() {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => this.setState({ data }));
  }
  ```

### 2. 更新阶段（Updating）

更新阶段是指组件的 `props` 或 `state` 发生变化时，组件重新渲染的过程。在这个阶段，组件会依次调用以下方法：

#### 2.1 `static getDerivedStateFromProps(props, state)`

- **作用**：在组件更新之前调用，用于根据 `props` 更新 `state`。

- **调用时机**：组件更新之前。

- **返回值**：返回一个对象，用于更新 `state`。

- **示例**：

  jsx复制

  ```jsx
  static getDerivedStateFromProps(props, state) {
    if (props.value !== state.value) {
      return { value: props.value };
    }
    return null;
  }
  ```

#### 2.2 `shouldComponentUpdate(nextProps, nextState)`

- **作用**：决定组件是否需要重新渲染。

- **调用时机**：组件更新之前。

- **返回值**：返回 `true` 或 `false`，默认返回 `true`。

- **示例**：

  jsx复制

  ```jsx
  shouldComponentUpdate(nextProps, nextState) {
    return nextState.count !== this.state.count;
  }
  ```

#### 2.3 `render()`

- **作用**：返回组件的 JSX 结构，用于重新渲染到 DOM 中。

- **调用时机**：组件更新时。

- **示例**：

  jsx复制

  ```jsx
  render() {
    return <div>{this.state.count}</div>;
  }
  ```

#### 2.4 `getSnapshotBeforeUpdate(prevProps, prevState)`

- **作用**：在组件更新之前捕获 DOM 的状态，返回的值会作为参数传递给 `componentDidUpdate`。

- **调用时机**：组件更新之前。

- **返回值**：返回一个值，用于传递给 `componentDidUpdate`。

- **示例**：

  jsx复制

  ```jsx
  getSnapshotBeforeUpdate(prevProps, prevState) {
    if (prevProps.count !== this.props.count) {
      return this.someDOMElement.scrollHeight;
    }
    return null;
  }
  ```

#### 2.5 `componentDidUpdate(prevProps, prevState, snapshot)`

- **作用**：组件更新完成后调用，通常用于执行副作用操作，如 DOM 操作、API 请求等。

- **调用时机**：组件更新完成后。

- **参数**：

  - `prevProps`：更新前的 `props`。
  - `prevState`：更新前的 `state`。
  - `snapshot`：`getSnapshotBeforeUpdate` 的返回值。

- **示例**：

  jsx复制

  ```jsx
  componentDidUpdate(prevProps, prevState, snapshot) {
    if (snapshot) {
      this.someDOMElement.scrollTop = this.someDOMElement.scrollHeight;
    }
  }
  ```

### 3. 卸载阶段（Unmounting）

卸载阶段是指组件从 DOM 中移除的过程。在这个阶段，组件会调用以下方法：

#### 3.1 `componentWillUnmount()`

- **作用**：组件卸载之前调用，通常用于清理资源，如取消订阅、清除定时器等。

- **调用时机**：组件卸载之前。

- **示例**：

  jsx复制

  ```jsx
  componentWillUnmount() {
    clearInterval(this.timer);
  }
  ```

### 4. 错误处理

React 提供了两个生命周期方法，用于处理组件的错误：

#### 4.1 `static getDerivedStateFromError(error)`

- **作用**：在组件捕获到错误后，返回一个对象来更新 `state`。

- **调用时机**：组件捕获到错误后。

- **返回值**：返回一个对象，用于更新 `state`。

- **示例**：

  jsx复制

  ```jsx
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  ```

#### 4.2 `componentDidCatch(error, info)`

- **作用**：组件捕获到错误后调用，通常用于记录错误信息。

- **调用时机**：组件捕获到错误后。

- **参数**：

  - `error`：捕获到的错误。
  - `info`：包含组件堆栈信息的对象。

- **示例**：

  jsx复制

  ```jsx
  componentDidCatch(error, info) {
    logErrorToMyService(error, info);
  }
  ```

### 总结

React 的生命周期方法允许你在组件的不同阶段执行代码，从而实现复杂的逻辑。以下是生命周期方法的调用顺序：

1. **挂载阶段**：
   - `constructor`
   - `static getDerivedStateFromProps`
   - `render`
   - `componentDidMount`
2. **更新阶段**：
   - `static getDerivedStateFromProps`
   - `shouldComponentUpdate`
   - `render`
   - `getSnapshotBeforeUpdate`
   - `componentDidUpdate`
3. **卸载阶段**：
   - `componentWillUnmount`
4. **错误处理**：
   - `static getDerivedStateFromError`
   - `componentDidCatch`

## 添加事件侦听器

`componentDidMount()` 方法也是添加特定功能所需的任何事件监听器的最佳位置。 React 提供了一个合成事件系统，它封装了浏览器中的事件系统。 这意味着，不管用户用的是什么浏览器，合成事件系统的行为都完全相同 -- 即使不同浏览器之间的本地事件的行为可能不同。

之前已经接触了一些合成事件处理程序，如`onClick()`。 React 的合成事件系统非常适合用于在 DOM 元素上管理的大多数交互。 但是，如果要将事件处理程序附加到 document 或 window 对象，则必须直接执行此操作。

添加事件侦听器

在 `componentDidMount()` 方法中为 `keydown` 事件添加事件监听器，并让这些事件触发回调 `handleKeyPress()`。 可以使用 `document.addEventListener()`，它将事件（用引号括起来）作为第一个参数，将回调作为第二个参数。

```jsx

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
  }

  // 修改这行下面的代码
  componentDidMount() {
    // 添加 keydown 事件监听器
    document.addEventListener('keydown', this.handleKeyPress);
  }

  componentWillUnmount() {
    // 移除 keydown 事件监听器
    document.removeEventListener('keydown', this.handleKeyPress);
  }
  // 修改这行上面的代码

  handleEnter() {
    this.setState((state) => ({
      message: state.message + 'You pressed the enter key! '
    }));
  }

  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};


```

## 使用 shouldComponentUpdate 优化重新渲染

到目前为止，如果任何组件接收到新的 `state` 或新的 `props`，它会重新渲染自己及其所有子组件。 这通常是好的。 但是 React 提供了一种生命周期方法，当子组件接收到新的 `state` 或 `props` 时，可以调用该方法，并特别声明组件是否应该更新。 这个方法就是 `shouldComponentUpdate()`，它将 `nextProps` 和 `nextState` 作为参数。

这种方法是优化性能的有效方法。 例如，默认行为是，当组件接收到新的 `props` 时，即使 `props` 没有改变，它也会重新渲染。 可以通过使用 `shouldComponentUpdate()` 比较 `props` 来防止这种情况发生。 该方法必须返回一个 `boolean`（布尔值），该值告诉 React 是否更新组件。 可以比较当前的 props（`this.props`）和下一个 props（`nextProps`），以确定你是否需要更新，并相应地返回 `true` 或 `false`。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }

  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    // 只有在 nextProps.value 为偶数时，才返回 true
    return nextProps.value % 2 === 0;
  }

  componentDidUpdate() {
    console.log('Component re-rendered.');
  }

  render() {
    return <h1>{this.props.value}</h1>;
  }
}

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }

  addValue() {
    this.setState(state => ({
      value: state.value + 1
    }));
  }

  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value} />
      </div>
    );
  }
}

// 渲染 Controller 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<Controller />, document.getElementById('challenge-node'));
```

## 介绍内联样式

还有其他复杂的概念可以为 React 代码增加强大的功能。 但是，你可能会想知道更简单的问题，比如：如何对在 React 中创建的 JSX 元素添加样式。 你可能知道，鉴于[将 class 应用于 JSX 元素的方式](https://wia.pub/chinese/learn/front-end-development-libraries/react/define-an-html-class-in-jsx)，它与使用 HTML 并不完全相同。

如果从样式表导入样式，它就没有太大的不同。 使用 `className` 属性将 class 应用于 JSX 元素，并将样式应用于样式表中的 class。 另一种选择是使用内联样式，这在 ReactJS 开发中非常常见。

将内联样式应用于 JSX 元素，类似于在 HTML 中的操作方式，但有一些 JSX 差异。 以下是 HTML 中内联样式的示例：

```jsx
<div style="color: yellow; font-size: 16px">Mellow Yellow</div>
```

JSX 元素使用 `style` 属性，但是鉴于 JSX 的编译方式，不能将值设置为 `string`（字符串）。 相反，你应该将其设置为等于 JavaScript `object` 。 如下所示：

```jsx
<div style={{color: "yellow", fontSize: 16}}>Mellow Yellow</div>
```

注意到如何驼峰拼写 `fontSize` 属性了吗？ 这是因为 React 不接受样式对象中的 kebab-case 键。 React 将在 HTML 中为应用正确的属性名称。

介绍内联样式

在代码编辑器中给 `div` 添加一个 `style` 属性，将文本颜色设置为红色，字体大小设置为 `72px`。

Note that you can optionally set the font size to be a number, omitting the units `px`, or write it as `"72px"`.

（注意字体大小要用72或者"72px"）

```jsx
class Colorful extends React.Component {
  render() {
    return (
      <div style={{color: "red", fontSize: 72}}>Big Red</div>
    );
  }
};
```

## 在 React 中添加内联样式

在上一次挑战中，你可能已经注意到，除了设置为 JavaScript 对象的 `style` 属性之外，与 HTML 内联样式相比，React 的内联样式还有其他几个语法差异。 首先，某些 CSS 样式属性的名称使用驼峰式命名。 例如，最后一个挑战用 `fontSize` 而不是 `font-size` 来设置字体的大小。 对于 JavaScript 对象属性来说，像 `font-size` 这样的连字符命名是无效的语法，所以 React 使用驼峰式命名。 通常，任何连字符的 style 属性在 JSX 中都是使用驼峰式命名的。

除非另有规定，否则所有属性值长度单位（如 `height`、`width` 和 `fontSize`）都假定为 `px`。 例如，如果要使用 `em`，可以用引号将值和单位括起来，例如 `{fontSize: "4em"}`。 除了默认为 `px` 的长度值之外，所有其他属性值都应该用引号括起来。

在 React 中添加内联样式

如果你有大量样式，你可以将样式 `object`（对象）分配给一个常量，以保持代码组织有序。 在文件顶部将你的样式声明为全局变量。 定义一个 `styles` 常量，并将其声明为具有三个样式属性及对应值的 `object`（对象）。 使 `div` 的文字颜色为 `purple`、字体大小为 `40`、边框为 `2px solid purple`。 然后设置 `style` 属性，使其等于 `styles` 常量。

样式复用就利用常量定义就行，要使用就直接<div style={styles}>Style Me!</div>

```jsx 

// 定义 styles 常量
const styles = {
  color: 'purple', // 设置文字颜色为 purple
  fontSize: 40,   // 设置字体大小为 40
  border: '2px solid purple' // 设置边框为 2px solid purple
};

class Colorful extends React.Component {
  render() {
    // 使用 styles 常量设置 div 的样式
    return (
      <div style={styles}>Style Me!</div>
    );
  }
};
```

## 在 React Render 方法中使用 JavaScript

在之前的挑战中，你学习了如何使用大括号 `{ }` 将 JavaScript 代码插入到 JSX 代码中，用于访问 props、传递 props、访问 state、在代码中插入注释以及最近学习的定制组件样式等任务。 这些都是将 JavaScript 放在 JSX 中的常见用例，但是在 React 组件中使用 JavaScript 代码还有其他方式。

在 `render` 方法中编写 JavaScript，可以把 JavaScript 直接放在 `return` 语句之前，而***不必***将其插入大括号中。 这是因为它还不在 JSX 代码中。 如果之后想在 `return` 语句中的 JSX 代码*里面*使用变量时，可以将变量名放在大括号中。

在 React Render 方法中使用 JavaScript

在提供的代码中，`render` 方法中有一个包含 20 个短语的数组，用于表示 20 世纪 80 年代经典魔术八球玩具中的答案。 绑定 `ask` 方法到按钮的单击事件，每次单击该按钮时，将生成随机数并将其存储为 state 中的 `randomIndex`。 在第 52 行，删除字符串 `change me!` 并重新分配 `answer` 常量，以便每次组件更新时，代码随机访问 `possibleAnswers` 数组的不同值。 最后，在 `p` 标签内插入 `answer` 常量。

```jsx
const inputStyle = {
  width: 235,
  margin: 5
};

class MagicEightBall extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: '',
      randomIndex: ''
    };
    this.ask = this.ask.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  ask() {
    if (this.state.userInput) {
      this.setState({
        randomIndex: Math.floor(Math.random() * 20),
        userInput: ''
      });
    }
  }
  handleChange(event) {
    this.setState({
      userInput: event.target.value
    });
  }
  render() {
    const possibleAnswers = [
      'It is certain',
      'It is decidedly so',
      'Without a doubt',
      'Yes, definitely',
      'You may rely on it',
      'As I see it, yes',
      'Outlook good',
      'Yes',
      'Signs point to yes',
      'Reply hazy try again',
      'Ask again later',
      'Better not tell you now',
      'Cannot predict now',
      'Concentrate and ask again',
      "Don't count on it",
      'My reply is no',
      'My sources say no',
      'Most likely',
      'Outlook not so good',
      'Very doubtful'
    ];
     // 根据 randomIndex 获取答案，如果没有 randomIndex，则显示空字符串
    const answer = this.state.randomIndex !== '' ? possibleAnswers[this.state.randomIndex] : '';
    return (
      <div>
        <input
          type='text'
          value={this.state.userInput}
          onChange={this.handleChange}
          style={inputStyle}
        />
        <br />
        <button onClick={this.ask}>Ask the Magic Eight Ball!</button>
        <br />
        <h3>Answer:</h3>
        <p>{answer}</p>
      </div>
    );
  }
}
```

注意： <p>{answer} </p>不算空的p元素，因为多了空格， <p>{answer}</p>才是真正可以空的p元素

## 使用 If-Else 条件进行渲染

使用 JavaScript 控制渲染视图的另一个应用是按条件渲染元素。 当条件为真时，将呈现一个视图， 反之，则呈现另一种视图。 可以在 React 组件的 `render()` 方法中使用的标准 `if/else` 语句来实现这一点。

使用 If-Else 条件进行渲染

MyComponent 的 state 中包含一个 `boolean`（布尔值），用于跟踪是否要在 UI 中显示某个元素。 `button` 切换此值的状态。 目前，它每次都呈现相同的 UI。 用 `if/else` 语句重写 `render()` 方法，如果 `display` 为 `true` 则返回当前标记。 否则，返回不带 `h1` 元素的标记。

**注意：** 写 `if/else` 语句才能通过测试， 使用三元运算符是不会通过的。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    };
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }

  toggleDisplay() {
    this.setState((state) => ({
      display: !state.display
    }));
  }

  render() {
    // 使用 if/else 语句进行条件渲染
    if (this.state.display) {
      return (
        <div>
          <button onClick={this.toggleDisplay}>Toggle Display</button>
          <h1>Displayed!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleDisplay}>Toggle Display</button>
        </div>
      );
    }
  }
}

```

## 使用 && 获得更简洁的条件

`if/else` 语句在上一次挑战中是有效的，但是有一种更简洁的方法可以达到同样的结果。 假设正在跟踪组件中的几个条件，并且希望根据这些条件中的每一个来渲染不同的元素。 如果你写了很多 `else if` 语句来返回稍微不同的 UI，你可能会写很多重复代码，这就留下了出错的空间。 相反，你可以使用 `&&` 逻辑运算符以更简洁的方式执行条件逻辑。 这是完全可行的，因为你希望检查条件是否为 `true`。如果是，则返回一些标记。 下面是一个示例：

```jsx
{condition && <p>markup</p>}
```

如果 `condition` 为 `true`，则返回标记。 如果条件为 `false` ，则在评估 `condition` 后操作将立即返回 `false`，并且不返回任何内容。 可以将这些语句直接包含在 JSX 中，并通过在每个条件后面写 `&&` 来将多个条件串在一起。 这允许你在 `render()` 方法中处理更复杂的条件逻辑，而无需重复大量代码。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    };
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }

  toggleDisplay() {
    this.setState((state) => ({
      display: !state.display
    }));
  }

  render() {
    return (
      <div>
        <button onClick={this.toggleDisplay}>Toggle Display</button>
        {this.state.display && <h1>Displayed!</h1>}
      </div>
    );
  }
}

// 渲染 MyComponent 到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<MyComponent />, document.getElementById('challenge-node'));
```

## 使用三元表达式进行条件渲染

在继续使用动态渲染技术之前，还有最后一种方法可以渲染想要的东西，它使用内置的 JavaScript 条件：三元运算符。 三元运算符经常被用作 JavaScript 中 `if/else` 语句的缩写。 它们不像传统的 `if/else` 语句那样强大，但是在 React 开发人员中非常流行， 原因之一就是 JSX 的编译原理，`if/else` 语句不能直接插入到 JSX 代码中。 可能你在前几个挑战就注意到了这一点——当需要 `if/else` 语句时，它总是在 `return` 语句的*外面*。 如果想在 JSX 中实现条件逻辑，三元表达式是一个很好的选择。 回想一下，三元运算符有三个部分，但是可以将多个三元表达式组合在一起。 以下是基本语法：

```jsx
condition ? expressionIfTrue : expressionIfFalse;
```

使用三元表达式进行条件渲染

代码编辑器在 `CheckUserAge` 组件的 `render()` 方法中定义了三个常量， 它们分别是 `buttonOne`、`buttonTwo` 和 `buttonThree`。 每个都分配了一个表示按钮元素的简单 JSX 表达式。 首先，使用 `input` 和 `userAge` 初始化 `CheckUserAge` 的 state，并将其值设置为空字符串。

一旦组件将信息渲染给页面，用户应该有一种方法与之交互。 在组件的 `return` 语句中，设置一个实现以下逻辑的三元表达式：当页面首次加载时，将提交按钮 `buttonOne` 渲染到页面。 然后，当用户输入年龄并点击该按钮时，根据年龄渲染不同的按钮。 如果用户输入的数字小于`18`，则渲染`buttonThree`。 如果用户输入的数字大于或等于`18`，则渲染`buttonTwo`。



```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const inputStyle = {
  width: 235,
  margin: 5
};

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    // 初始化 state
    this.state = {
      input: '', // 用户输入的年龄
      userAge: '' // 最终提交的年龄
    };
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.setState({
      input: e.target.value,
      userAge: '' // 清空 userAge，以便重新输入
    });
  }

  submit() {
    this.setState(state => ({
      userAge: state.input // 将输入的年龄设置为 userAge
    }));
  }

  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;

    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type='number'
          value={this.state.input}
          onChange={this.handleChange}
        />
        <br />
        {/* 使用三元表达式进行条件渲染 */}
        {this.state.userAge === '' ? buttonOne : 
          (parseInt(this.state.userAge, 10) >= 18 ? buttonTwo : buttonThree)}
      </div>
    );
  }
}

// 渲染 CheckUserAge 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<CheckUserAge />, document.getElementById('challenge-node'));
```

## 使用 Props 有条件地渲染

到目前为止，你已经了解了如何使用 `if/else`、`&&` 和三元运算符（`condition ? expressionIfTrue : expressionIfFalse`）来决定渲染什么和何时渲染。 然而，还有一个重要的话题需要讨论，它可以让你将这些概念中的一个或所有与另一个强大的 React 特性结合起来：props。 使用 props 有条件地渲染代码对于 React 开发人员来说非常常见——也就是说，他们使用给定 props 的值来自动决定要渲染什么。

在这个挑战中，将设置一个子组件来根据 props 做出渲染决定。 可以使用三元运算符，但是可以看到过去几个挑战中涵盖的其他几个概念在这种情况下可能同样有用。

使用 Props 有条件地渲染

代码编辑器有两个部分定义了的组件：一个名为 `GameOfChance` 的父组件和一个名为 `Results` 的子组件。 它们被用来创建一个简单的游戏，用户按下按钮来看它们是赢还是输。

首先，需要一个简单的表达式，每次运行时都会随机返回一个不同的值。 可以使用 `Math.random()`。 每次调用此方法时，此方法返回 `0`（包括）和 `1`（不包括）之间的值。 因此，对于 50/50 的几率，请在表达式中使用 `Math.random() >= .5`。 从统计学上讲，这个表达式有 50％ 的几率返回 `true`，另外 50％ 返回 `false`。 在 render 方法里，用此表达式替换 `null` 以完成变量声明。

现在你有了一个表达式，可以使用该表达式在代码中做出随机决策。 接下来，需要实现此功能。 将 `Results` 组件渲染为 `GameOfChance` 的子 组件，并将 `expression` 作为名为 `fiftyFifty` 的 prop 传入 。 在 `Results` 组件中，编写一个三元表达式来渲染 `h1` 元素的文本。`GameOfChance` 传来的 prop `fiftyFifty` 来决定渲染文本 `You Win!` 还是 `You Lose!`。 最后，确保 `handleClick()` 方法正确计算每个回合，以便用户知道他们玩过多少次。 这也可以让用户知道组件实际上已经更新，以防他们连续赢两次或输两次时自己不知道。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Results extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    // 使用三元表达式根据 fiftyFifty 的值渲染不同的文本
    return <h1>{this.props.fiftyFifty ? 'You Win!' : 'You Lose!'}</h1>;
  }
}

class GameOfChance extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 1
    };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      counter: prevState.counter + 1 // 每次点击按钮，counter 加 1
    }));
  }

  render() {
    // 使用 Math.random() 生成一个随机值，50% 的几率返回 true 或 false
    const expression = Math.random() >= 0.5;

    return (
      <div>
        <button onClick={this.handleClick}>Play Again</button>
        {/* 将 expression 作为 fiftyFifty 属性传递给 Results 组件 */}
        <Results fiftyFifty={expression} />
        <p>{'Turn: ' + this.state.counter}</p>
      </div>
    );
  }
}

// 渲染 GameOfChance 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<GameOfChance />, document.getElementById('challenge-node'));
```

## 根据组件状态有条件地更改内联 CSS

此时，已经看到了一些条件渲染的应用程序和内联样式的使用。 这里还有一个将这两个主题结合在一起的例子。 你也可以根据 React 组件的 state 有条件地渲染 CSS。 要执行此操作，请检查条件，如果满足该条件，则修改在 render 方法中分配给 JSX 元素的样式对象。

理解这个模式很重要，因为相比传统的方式（这在 jQuery 中非常常见），直接修改 DOM 元素来应用样式的方法是一个戏剧性的转变。 在该方法中，必须跟踪元素何时更改并直接处理实际操作。 跟踪更改可能变得很困难，可能会使 UI无法预测。 当根据一个条件设置一个样式对象时，描述了 UI 作为应用程序的状态函数应当如何展现。 如此便有一个清晰的单向流动的信息流。 这是使用 React 编写应用程序时的首选方法。

根据组件状态有条件地更改内联 CSS

代码编辑器有一个简单的带有边框样式的受控 input 组件。 如果用户在输入框中键入超过 15 个字符的文本，希望将此边框变成红色。 添加一个条件来检查这一点，如果条件有效，则将 input 的边框样式设置为`3px solid red`。 可以通过在 input 中输入文本来检测它。

```jsx
class GateKeeper extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(event) {
    this.setState({ input: event.target.value });
  }

  render() {
    let inputStyle = {
      border: '1px solid black'
    };

    // 如果输入框中的文本长度超过 15 个字符，改变边框样式
    if (this.state.input.length > 15) {
      inputStyle.border = '3px solid red';
    }

    return (
      <div>
        <h3>Don't Type Too Much:</h3>
        <input
          type="text"
          style={inputStyle}
          value={this.state.input}
          onChange={this.handleChange}
        />
      </div>
    );
  }
}
```

## 使用 Array.map() 动态渲染元素

条件渲染很有用，但是可能需要组件来渲染未知数量的元素。 通常在响应式编程中，程序员在应用程序运行时之前无法知道其 state，因为这在很大程度上取决于用户与该程序的交互。 程序员需要提前编写代码来正确处理未知状态。 在 React 中使用 `Array.map()` 阐明了这个概念。

例如，创建一个简单的 “To Do List” 应用程序。 作为程序员，你无法知道用户可能在其列表中有多少项。 需要设置组件，以便在使用该程序的人决定今日待办事项之前动态渲染列表元素的正确数量。

使用 Array.map() 动态渲染元素

代码编辑器完成了 `MyToDoList` 组件的大部分设置。 如果完成了受控表单挑战，这些代码中的一些应该看起来很熟悉。 你会注意到一个 `textarea` 和一个 `button`，以及一些跟踪它们状态的方法，但是页面当前还没有任何东西被渲染。

在 `constructor` 中，创建一个 `this.state` 对象并定义两个 state：`userInput` 应该初始化为空字符串，`toDoList` 应该初始化为空数组。 接下来，在 `render()` 方法中删除 `items` 变量的 `null` 值。 取而代之的是，将存储在组件内部 state 中的 `toDoList` 数组一一遍历，并相应地动态呈现在 `li` 元素中。 尝试在 `textarea` 中输入 `eat, code, sleep, repeat`，然后点击按钮，看看会发生什么。

**注意：** 像这样的映射操作创建的所有兄弟子元素都需要提供唯一的 `key` 属性。 别担心，这是下一个挑战的主题。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const textAreaStyles = {
  width: 235,
  margin: 5
};

class MyToDoList extends React.Component {
  constructor(props) {
    super(props);
    // 初始化 state
    this.state = {
      userInput: '',
      toDoList: []
    };
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }

  handleSubmit() {
    const itemsArray = this.state.userInput.split(',').map(item => item.trim());
    this.setState({
      toDoList: itemsArray
    });
  }

  handleChange(e) {
    this.setState({
      userInput: e.target.value
    });
  }

  render() {
    // 使用 Array.map() 动态渲染 toDoList 中的每个项目
    const items = this.state.toDoList.map((item, index) => (
      <li key={index}>{item}</li>
    ));

    return (
      <div>
        <textarea
          onChange={this.handleChange}
          value={this.state.userInput}
          style={textAreaStyles}
          placeholder='Separate Items With Commas'
        />
        <br />
        <button onClick={this.handleSubmit}>Create List</button>
        <h1>My "To Do" List:</h1>
        <ul>{items}</ul>
      </div>
    );
  }
}

// 渲染 MyToDoList 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<MyToDoList />, document.getElementById('challenge-node'));
```

## 给同级元素一个唯一的键属性

上一个挑战展示了如何使用 `map` 方法根据用户输入动态渲染多个元素。 然而，这个例子中缺少一个重要的部分。 创建元素数组时，每个元素都需要一个设置为唯一值的 `key` 属性。 React 使用这些键来跟踪哪些项目被添加、更改或删除。 这有助于在以任何方式修改列表时提高重新渲染过程的效率。

**注意：** 键只需要在兄弟元素之间是唯一的，它们不需要在应用程序中是全局唯一的。

给同级元素一个唯一的键属性

代码编辑器有一个数组，它包含一些前端框架和一个名为 `Frameworks()` 的无状态函数组件。 `Frameworks()` 需要将数组映射到无序列表，就像上一个挑战一样。 完成 `map` 回调，为 `frontEndFrameworks` 数组中的每个框架返回一个 `li` 元素。 这次，确保给每个 `li` 的 `key` 属性设置一个唯一的值。 `li` 元素还应该包含来自 `frontEndFrameworks` 的文本。

通常，希望使 key 能唯一标识要渲染的元素。 数组索引可以是最后的选择，但通常你应该尝试使用唯一标识。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const frontEndFrameworks = [
  'React',
  'Angular',
  'Ember',
  'Knockout',
  'Backbone',
  'Vue'
];

function Frameworks() {
  // 使用 Array.map() 方法将数组中的每个框架映射为一个 <li> 元素
  const renderFrameworks = frontEndFrameworks.map((framework, index) => (
    <li key={framework}>{framework}</li> // 使用框架名称作为 key
  ));

  return (
    <div>
      <h1>Popular Front End JavaScript Frameworks</h1>
      <ul>
        {renderFrameworks}
      </ul>
    </div>
  );
}

// 渲染 Frameworks 组件到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<Frameworks />, document.getElementById('challenge-node'));
```

## 使用 Array.Filter() 动态过滤数组

`map` 数组方法是一个强大的工具，在使用 React 时经常使用。 与 `map` 相关的另一种方法是 `filter`，它根据条件过滤数组的内容，然后返回一个新数组。 例如，如果有一个 users 数组，每个数组元素都有一个可以设置为 `true` 或 `false` 的 `online` 属性，可以这样只过滤那些在线的用户：

```js
let onlineUsers = users.filter(user => user.online);
```

使用 Array.Filter() 动态过滤数组

在代码编辑器中，`MyComponent` 的 `state` 被初始化为一个用户数组。 有些用户在线，有些则没有。 过滤数组，以便只查看在线用户。 要执行此操作，请首先使用 `filter` 返回仅包含 `online` 属性为 `true` 的用户的新数组。 然后，在 `renderOnline` 变量中，映射已过滤的数组，并为包含其 `username` 文本的每个用户返回 `li` 元素。 确保包含一个唯一的 `key`，就像上一个挑战一样。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      users: [
        {
          username: 'Jeff',
          online: true
        },
        {
          username: 'Alan',
          online: false
        },
        {
          username: 'Mary',
          online: true
        },
        {
          username: 'Jim',
          online: false
        },
        {
          username: 'Sara',
          online: true
        },
        {
          username: 'Laura',
          online: true
        }
      ]
    };
  }

  render() {
    // 使用 filter 方法过滤在线用户
    const usersOnline = this.state.users.filter(user => user.online);

    // 使用 map 方法将过滤后的用户数组映射为 <li> 元素
    const renderOnline = usersOnline.map((user, index) => (
      <li key={index}>{user.username}</li>
    ));

    return (
      <div>
        <h1>Current Online Users:</h1>
        <ul>{renderOnline}</ul>
      </div>
    );
  }
}

// 渲染 MyComponent 到 DOM 中的 id='challenge-node' 的 div
ReactDOM.render(<MyComponent />, document.getElementById('challenge-node'));
```

## 用 renderToString 在服务器上渲染 React

到目前为止，已经能够在客户端上渲染 React 组件， 一般来说我们都是这么做的。 然而，在一些用例中，需要在服务器上渲染一个 React 组件。 由于 React 是一个 JavaScript 视图库，所以通常使用 Node 让 JavaScript 运行在服务器上。 事实上，React 提供了一个可用于此目的的 `renderToString()` 方法。

有两个关键原因可以解释为什么服务器上的渲染可能会在真实世界的应用程序中使用。 首先，如果不这样做，当 React 应用程序最初加载到浏览器时，它将包含一个代码量很少的 HTML 文件和一大堆 JavaScript。 这对于搜索引擎来说可能不太理想，因为它们试图为网页内容生成索引，以便人们可以找到这个应用。 如果在服务器上渲染初始 HTML 标记并将其发送到客户端，则初始页面加载的内容包含搜索引擎可以抓取的所有页面标记。 其次，这创造了更快的初始页面加载体验，因为渲染的 HTML 代码量要比整个应用程序的 JavaScript 代码小。 React 仍然能够识别你的应用并在初始加载后进行管理。

用 renderToString 在服务器上渲染 React

`renderToString()` 方法由 `ReactDOMServer` 提供，在这里已为你定义成全局变量。 这个方法接收一个 React 元素作为参数。 用它来把 `App` 渲染成字符串。

```jsx
import React from 'react';
import ReactDOMServer from 'react-dom/server';

class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <div>My App</div>;
  }
};

// 使用 ReactDOMServer.renderToString 将 App 渲染为字符串
const appString = ReactDOMServer.renderToString(<App />);
console.log(appString);
```

# Vue复习

## 创建一个简单的模板

### 什么是 Vue？

Vue (发音为 /vjuː/，类似 view) 是一款用于构建用户界面的 JavaScript 框架。它基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面。

前端框架主要以React为主，但 Vue 在中国非常流行，因为它是中国尤雨溪（Evan You）创建的，尤雨溪毕业于科尔盖特大学，曾就职于Google Creative Labs和Meteor Development Group。由于工作中大量接触开源的JavaScript项目，最后自己也走上了开源之路，现全职开发和维护Vue.js。

与React在js代码中完成html（jsx）相反，Vue在html中通过声明式完成js功能。因此，在Html、Css和js之外，需要学习一套新的模板语法。

### Vue 的两个核心功能：

- 声明式渲染：Vue 基于标准 HTML 拓展了一套模板语法，使得我们可以声明式地描述最终输出的 HTML 和 JavaScript 状态之间的关系。
- 响应性：Vue 会自动跟踪 JavaScript 状态并在其发生变化时响应式地更新 DOM。

你可能已经有了些疑问——先别急，在后续的文档中我们会详细介绍每一个细节。现在，请继续看下去，以确保你对 Vue 作为一个框架到底提供了什么有一个宏观的了解。

### 预备知识

> 学习完 HTML、CSS 和 JavaScript 后继续本课程。如果你对前端开发完全陌生，最好不要直接从一个框架开始进行入门学习——最好是掌握了基础知识再回到这里。如果之前有其他框架的经验会很有帮助，但也不是必须的。

Vue 的模板使用`<template>`标签，如：

```js
<template>
  <div>Hello World!</div>
</template>
```

### 应用实例

有了Vue模板，就可以通过`createApp` 函数创建一个应用实例，并加载到Html页面：

```js
import { createApp } from 'vue'

const app = createApp({
  /* 根组件选项 */
})

app.mount('#挂载层')
```

值得注意的是，Vue挑战已通过`<script src="https://cdn.staticfile.net/vue/3.3.4/vue.global.prod.min.js"></script>` 将Vue加载到浏览器的全局环境中（挂载在window对象下）。

挑战在底层调用`createApp(App).mount('#root')`将 组件挂载在Html页面id为`root`的`div`中。Vue将使用自己的 虚拟DOM对比算法来实现视图与数据的增量更新，并自带加载到Html页面。

### API 风格

Vue 的组件可以按两种不同的风格书写：`选项式 API` 和`组合式 API`。本挑战选用的是`选项式 API`。

**选项式 API (Options API)**

选项式 API，我们可以用包含多个选项的对象来描述组件的逻辑，例如 data、methods 和 mounted。选项所定义的属性都会暴露在函数内部的 this 上，它会指向当前的组件实例。

```js
<script>
export default {
  // data() 返回的属性将会成为响应式的状态
  // 并且暴露在 `this` 上
  data() {
    return {
      count: 0
    }
  },

  // methods 是一些用来更改状态与触发更新的函数
  // 它们可以在模板中作为事件处理器绑定
  methods: {
    increment() {
      this.count++
    }
  },

  // 生命周期钩子会在组件生命周期的各个不同阶段被调用
  // 例如这个函数就会在组件挂载完成后被调用
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

创建一个简单的模板

将 `div` 替换为 `h1` 元素，并在其中添加文本 `Hello Vue!`。

## 创建一个变量内容元素

### 声明式渲染

Vue 组件一般以单文件组件 (Single-File Component，缩写为 SFC)。SFC 是一种可复用的代码组织形式，它将从属于同一个组件的 HTML、CSS 和 JavaScript 合并封装在单一 .vue 后缀的文件中。类似于React将HTML与JavaScript合并封装在单一 .jsx 后缀的文件中。

单文件模式有利于组件复用，但需学习额外的知识。React、Vue的流行，使单文件组件模式成为前端（Web App）研发主流。在各种原生应用研发中（桌面如VB、Delphi、CBC、VS等WinForm、WPF，手机如苹果原生、安卓原生等），普遍将代码、UI分离研发，最后打包合并发布。

随着Web组件标准的逐渐完备、成熟，Web App最终会替代原生应用，分离式研发，标准组件会成为主流，Vue和React终将退出历史舞台。

Vue 的核心功能是声明式渲染：通过扩展于标准 HTML 的模板语法，我们可以根据 JavaScript 的状态来描述 HTML 应该是什么样子的。当状态改变时，HTML 会自动更新。

能在改变时触发更新的状态被认为是响应式的。在 Vue 中，响应式状态被保存在组件中。 我们可以使用 `data` 组件选项来声明响应式状态，该选项应该是一个返回对象的函数：

```js
export default {
  data() {
    return {
      message: 'Hello World!'
    }
  }
}
```

message 属性可以在模板中使用。下面展示了我们如何使用`双花括号`法，根据 message 的值来渲染动态文本：

```
<h1>{{ message }}</h1>
```

在双花括号中的内容并不只限于标识符或路径——我们可以使用任何有效的 JavaScript 表达式。

```
<h1>{{ message.split('').reverse().join('') }}</h1>
```

现在，试着自己创建一个数据属性，用它来为模板中的 `<h1>` 渲染动态的文本内容。

创建一个变量内容元素

通过`msg`和`count`变量来定义模板生成页面。

**提示：** 请使用 `data()` 返回变量。

```vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <p>Count is: {{ count }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: 'Hello Vue!', // 定义 msg 变量，初始值为 'Hello Vue!'
      count: 0 // 定义 count 变量，初始值为 0
    };
  },
  methods: {
    increment() {
      this.count += 1; // 增加 count 的值
    }
  }
};
</script>

<style>
/* 添加一些样式 */
h1 {
  color: blue;
}
p {
  font-size: 18px;
}
button {
  margin-top: 10px;
  padding: 5px 10px;
  font-size: 16px;
}
</style>
```

## 创建一个简单的计数器

### 事件监听

我们可以使用 `v-on` 指令监听 DOM 事件：

```
<button v-on:click="click">{{ variable }}</button>
```

因为其经常使用，`v-on` 也有一个简写语法：

```
<button @click="click">{{ variable }}</button>
```

> 点评：react的点击事件是标准的`onClick`，而不是`v-on:click`，也不是`@click`，`vue`增加一个新的语法，似乎并无必要。所以相对于`react`的写代码，`vue`在`定义`代码，也就是`申明式语法`。

此处，`click` 引用了一个使用 `methods` 选项声明的函数：

```js
export default {
  data() {
    return {
      i: 0
    }
  },
  methods: {
    click() {
      // 更新组件状态
      this.i++
    }
  }
}
```

在方法中，我们可以使用 `this` 来访问组件实例。组件实例会暴露 data 中声明的数据属性。我们可以通过改变这些属性的值来更新组件状态。

事件处理函数也可以使用内置表达式，并且可以使用修饰符简化常见任务。这些细节包含在[指南 - 事件处理](https://cn.vuejs.org/guide/essentials/event-handling.html)。

创建一个简单的计数器

实现 `click` 方法增加计数，并通过使用 `v-on` 将其绑定到按钮上。

```vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <p>Count is: {{ count }}</p>
    <button v-on:click="increment">点击增加计数</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: 'Hello Vue!', // 定义 msg 变量
      count: 0 // 定义 count 变量
    };
  },
  methods: {
    increment() {
      this.count += 1; // 增加 count 的值
    }
  }
};
</script>

<style>
/* 添加一些样式 */
h1 {
  color: blue;
}
p {
  font-size: 18px;
}
button {
  margin-top: 10px;
  padding: 5px 10px;
  font-size: 16px;
}
</style>
```

## 元素属性绑定

### 元素属性（Attribute）绑定

在 Vue 中，mustache 语法 (即双大括号) 只能用于文本插值。为了给 attribute 绑定一个动态值，需要使用 `v-bind` 指令：

<div v-bind:id="dynamicId"></div>

指令是由 `v-`开头的一种特殊 attribute。它们是 Vue 模板语法的一部分。和文本插值类似，指令的值是可以访问组件状态的 JavaScript 表达式。关于 v-bind 和指令语法的完整细节请详阅[指南-模板语法](https://cn.vuejs.org/guide/essentials/template-syntax.html)。

冒号后面的部分 `(:id) `是指令的“参数”。此处，元素的 `id` attribute 将与组件状态里的 `dynamicId` 属性保持同步。

由于 `v-bind` 使用地非常频繁，它有一个专门的简写语法：

<div :id="dynamicId"></div>

**点评：** `react` 的 `jsx` 中没有额外增加属性绑定语法，使用的是统一的`{}`，`vue`将属性与内容的变量绑定分开，增加了新的语法，似乎并无必要。

元素属性绑定

现在，试着把一个动态的 `class` 绑定添加到这个 `<h1>` 上，并使用 `titleClass` 的数据属性作为它的值。如果绑定正确，文字将会变为红色。

```vue
<template>
  <h1 :class="titleClass">Make me red</h1> <!-- 动态绑定 class -->
</template>

<script>
export default {
  data() {
    return {
      titleClass: 'title' // 定义 titleClass 为 'title'
    };
  }
};
</script>

<style>
.title {
  color: red; /* 设置文字颜色为红色 */
}
</style>
```

