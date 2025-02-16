# SVELTE

## 基础

基本语法与vue相似

大括号里直接视为js语法，注意img标签必须有alt属性（就是图片不显示后显示的文本）

```svelte
<script>
	let src = '/tutorial/image.gif';
	let name= "stven"
</script>

<img src={src} alt="{name} dance"/>
<h1>
    Hello,{name}
</h1>

```

当然name 和 value 相同的 attribute 并不少见，比如 `src={src}`。Svelte 为这些情况提供了一个方便的简写：

```svelte
<img {src} alt="{name} dances." />
```

Just like in HTML, you can add a `<style>` tag to your component. Let’s add some styles to the `<p>` element:
就像在 HTML 中一样，您可以向组件添加 `<style>` 标签。让我们向 `<p>` 元素添加一些样式：

App 应用程序

```svelte
<p>This is a paragraph.</p>

<style>
	p {
		color: goldenrod;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

Importantly, these rules are *scoped to the component*. You won’t accidentally change the style of `<p>` elements elsewhere in your app, as we’ll see in the next step.
重要的是，这些规则*的范围仅限于组件*。您不会意外更改应用程序中其他位置的 `<p>` 元素的样式，我们将在下一步中看到。

注意这里尺寸用的em，em是相对长度单位，相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。em的值并不是固定的，会继承父级元素的字体大小。任意浏览器的默认字体高都是16px。所有未经调整的浏览器都符合：1em=16px

## 嵌套组件

在script标签中导入，在html中使用

It would be impractical to put your entire app in a single component. Instead, we can import components from other files and include them in our markup.
将整个应用程序放在单个组件中是不切实际的。相反，我们可以从其他文件导入组件并将它们包含在我们的标记中。

Add a `<script>` tag to the top of `App.svelte` that imports `Nested.svelte`...
在 `App.svelte` 的顶部添加一个 `<script>` 标签，该标签将导入 `Nested.svelte`...

App 应用程序

```svelte
<script lang="ts">
	import Nested from './Nested.svelte';
</script>
```

...and include a `<Nested />` component:
...并包含一个 `<Nested />` 组件：

App 应用程序

```svelte
<p>This is a paragraph.</p>
<Nested />
```

Notice that even though `Nested.svelte` has a `<p>` element, the styles from `App.svelte` don’t leak in.
请注意，即使 `Nested.svelte` 具有 `<p>` 元素，`App.svelte` 中的样式也不会泄漏。

**注意组件名称大写，以区别于 HTML 元素**。

## 解析变量为html标签

Ordinarily, strings are inserted as plain text, meaning that characters like `<` and `>` have no special meaning.
通常，字符串以纯文本形式插入，这意味着 `<` 和 `>` 等字符没有特殊含义。

But sometimes you need to render HTML directly into a component. For example, the words you’re reading right now exist in a markdown file that gets included on this page as a blob of HTML.
但有时你需要将 HTML 直接呈现到组件中。例如，你现在正在阅读的单词存在于 Markdown 文件中，该文件作为 HTML blob 包含在此页面上。

In Svelte, you do this with the special `{@html ...}` tag:
在 Svelte 中，您可以使用特殊的 `{@html ...}` 标签来执行此作：

App 应用程序

```svelte
<script>
	let string = `this string contains some <strong>HTML!!!</strong>`;
</script>

<p>{@html string}</p> //这样string变量里面的strong标签就能被正确解析
```

> Important: Svelte doesn’t perform any sanitization of the expression inside `{@html ...}` before it gets inserted into the DOM. This isn’t an issue if the content is something you trust like an article you wrote yourself. However if it’s some untrusted user content, e.g. a comment on an article, then it’s critical that you manually escape it, otherwise you risk exposing your users to [Cross-Site Scripting](https://owasp.org/www-community/attacks/xss/) (XSS) attacks.
> 重要提示：Svelte 在将 `{@html ...}` 中的表达式插入 DOM 之前不会对其进行任何清理。如果内容是您信任的，例如您自己写的文章，则这不是问题。但是，如果它是一些不受信任的用户内容，例如对文章的评论，那么手动转义它至关重要，否则您可能会使用户面临[跨站点脚本](https://owasp.org/www-community/attacks/xss/) （XSS） 攻击的风险。

## 响应式变量

类似ref，svelte通过使用 `$state（...）` 包装值，使 `count` 声明成为响应式的：

App 应用程序

```svelte
<script>
	let count = $state(0);

	function increment() {
		// TODO implement
		count +=1
	}
</script>

<button onclick={increment}>
	Clicked {count}
	<!-- 解析我为js语句 -->
	{count === 1 ? 'time' : 'times'}
</button>
```

This is called a *rune*, and it’s how you tell Svelte that `count` isn’t an ordinary variable. Runes look like functions, but they’re not — when you use Svelte, they’re part of the language itself.
这被称为 *rune*，它是你告诉 Svelte count 不是一个普通变量的方式。``Runes 看起来像函数，但事实并非如此——当你使用 Svelte 时，它们是语言本身的一部分。

All that’s left is to implement `increment`:
剩下的就是实现 `increment`

As we saw in the previous exercise, state reacts to *reassignments*. But it also reacts to *mutations* — we call this *deep reactivity*.
正如我们在上一个练习中看到的那样，state 对*重新分配*做出反应。但它也会对*突变*做出反应——我们称之为*深度反应*性。

Make `numbers` a reactive array:
将 `numbers` 设为响应式数组：

App 应用程序

```svelte
<script>
	let numbers = $state([1, 2, 3, 4]);
	let sum =$state(10)
	function getSum() {
		for(let i = 0;i<numbers.length;i++){
			sum += numbers[i]
		}
	}
	// 既然要用到getSum函数，那就要在调用它之前定义好它
	function addNumber() {
		// TODO implement
		numbers[numbers.length] = numbers.length + 1;
		getSum()
	}

</script>

<p>{numbers.join(' + ')} = {sum}</p>

<button onclick={addNumber} >
	Add a number
</button>

```

Now, when we change the array...
现在，当我们更改数组时...

App 应用程序

```svelte
function addNumber() {
	numbers[numbers.length] = numbers.length + 1;
}
```

...the component updates. Or better still, we can `push` to the array instead:
...组件将更新。或者更好的是，我们可以`改为推送到`数组：

App 应用程序

```svelte
function addNumber() {
	numbers.push(numbers.length + 1);
}
```

> Deep reactivity is implemented using [proxies](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy), and mutations to the proxy do not affect the original object.
> 深度响应性是使用 [proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 实现的，对 proxy 的更改不会影响原始对象。

即，响应式变量定义的数组还能自动扩充，对突变进行处理

## 数组reduce方法

这行代码在 Svelte 中使用了 `$derived` 语法来创建一个派生状态 `total`，它是基于 `numbers` 数组的动态计算结果。具体来说，它会监听 `numbers` 数组的变化，并实时计算数组中所有数字的总和。

### 代码解析

JavaScript复制

```javascript
let total = $derived(numbers.reduce((t, n) => t + n, 0));
```

#### 1. **`numbers.reduce` 方法**·	

`reduce` 是 JavaScript 数组的一个方法，用于对数组中的每个元素执行一个回调函数，并将结果累积到一个单一的值中。它的语法如下：

JavaScript复制

```javascript
array.reduce(callback, initialValue);
```

- **`callback`**：一个回调函数，接收两个参数：
  - **`accumulator`**（`t`）：累加器，保存当前的累积结果。
  - **`currentValue`**（`n`）：当前数组元素的值。
- **`initialValue`**：累加器的初始值。在这个例子中，初始值是 `0`。

在你的代码中：

JavaScript复制

```javascript
numbers.reduce((t, n) => t + n, 0)
```

- `t` 是累加器，初始值为 `0`。
- `n` 是数组中的当前元素。
- 每次回调函数执行时，将 `t` 和 `n` 相加，并将结果传递给下一次回调函数。
- 最终，`reduce` 方法返回数组中所有元素的总和。

#### 2. **`$derived` 语法**

`$derived` 是 Svelte 中用于创建派生状态的语法。它会自动监听依赖的响应式变量（在这个例子中是 `numbers`），并在依赖变量发生变化时重新计算派生状态。

- **`numbers`**：这是一个响应式变量，可能是一个数组，例如 `[1, 2, 3, 4]`。
- **`total`**：这是一个派生状态，它的值是 `numbers` 数组中所有数字的总和。

### 示例

假设 `numbers` 是一个响应式数组，代码如下：

JavaScript复制

```javascript
<script>
  import { derived } from 'svelte';

  let numbers = [1, 2, 3, 4]; // 初始值
  let total = $derived(numbers.reduce((t, n) => t + n, 0));
</script>

<p>Total: {total}</p>

<button on:click={() => numbers.push(5)}>Add 5</button>
```

#### **运行逻辑**

1. **初始状态**：
   - `numbers` 的值是 `[1, 2, 3, 4]`。
   - `total` 的值是 `1 + 2 + 3 + 4 = 10`。
   - 页面上显示 `Total: 10`。
2. **点击按钮**：
   - 点击按钮后，`numbers.push(5)` 将 `5` 添加到 `numbers` 数组中。
   - `numbers` 的值变为 `[1, 2, 3, 4, 5]`。
   - Svelte 的响应式系统会自动检测到 `numbers` 发生了变化，并重新计算 `total`。
   - `total` 的值变为 `1 + 2 + 3 + 4 + 5 = 15`。
   - 页面上更新显示 `Total: 15`。

### 总结

这行代码的作用是：

- 监听 `numbers` 数组的变化。
- 每次 `numbers` 发生变化时，自动计算数组中所有数字的总和，并将结果存储在 `total` 中。
- `total` 是一个派生状态，它的值会随着 `numbers` 的变化而动态更新。

这种方式利用了 Svelte 的响应式系统，使得代码更加简洁且易于维护。

## 派生状态（ *derive* state）（其实就是计算属性）

在 Svelte 中，**派生状态**是指基于组件的原始状态（如响应式变量或 props）通过计算或监听得到的派生数据。Svelte 提供了多种方式来处理派生状态，类似Vue里面的computed	主要包括**计算属性**和**侦听器**。

### 1. 计算属性

在 Svelte 中，计算属性可以通过 `derived` 函数或 `$:` 语法实现。

#### **使用 `derived` 函数**

`derived` 函数可以监听响应式变量的变化，并根据这些变化生成新的响应式值。

JavaScript复制

```javascript
<script>
  import { derived } from 'svelte';

  let count = 1;
  const doubleCount = derived(count, $count => $count * 2);
</script>

<p>{doubleCount}</p>
```

#### **使用 `$:` 语法**

`$:` 语法是 Svelte 提供的一种更简洁的方式，用于在变量发生变化时自动重新计算。

JavaScript复制

```javascript
<script>
  let count = 1;

  // 使用 $: 语法自动重新计算
  $: doubleCount = count * 2;
</script>

<p>{doubleCount}</p>
```

#### **特点**

- **自动更新**：当依赖的响应式变量发生变化时，计算属性会自动重新计算。
- **性能优化**：Svelte 的响应式系统会智能地处理依赖关系，避免不必要的计算。

### 2. 侦听器

侦听器用于监听响应式变量的变化，并在变化时执行特定的逻辑。

#### **使用 `$:` 语法**

`$:` 语法不仅可以用于计算属性，还可以用于执行副作用（如异步操作）。

JavaScript复制

```javascript
<script>
  let count = 1;

  // 监听 count 的变化
  $: {
    console.log(`Count changed to ${count}`);
  }
</script>
```

#### **使用 `$effect`**

在 Svelte 5 中，可以使用 `$effect` 来定义副作用，类似于 Vue 中的 `watchEffect`。

JavaScript复制

```javascript
<script>
  let count = 1;

  $effect(() => {
    console.log(`Count changed to ${count}`);
  });
</script>
```

### 3. 派生状态的使用场景

- **计算属性**：适用于基于依赖数据动态生成派生状态，如计算总价、格式化数据等。
- **侦听器**：适用于在数据变化时执行异步操作或复杂的逻辑，如保存数据到本地存储、发送网络请求等。

### 总结

在 Svelte 中，派生状态可以通过计算属性和侦听器实现。计算属性用于基于依赖数据动态生成派生状态，而侦听器用于在数据变化时执行特定逻辑。根据具体需求选择合适的方式可以提升代码的可维护性和性能。

​	Often, you will need to *derive* state from other state. For this, we have the `$derived` rune:
通常，您需要从其他状态*派生* state。为此，我们有 `$derived` rune：

App 应用程序

```
let numbers = $state([1, 2, 3, 4]);
let total = $derived(numbers.reduce((t, n) => t + n, 0));
```

We can now use this in our markup:
我们现在可以在我们的标记中使用它：

App 应用程序

```svelte
<script>
	let numbers = $state([1, 2, 3, 4]);
	let total = $derived(numbers.reduce((t, n) => t + n, 0));

	function addNumber() {
		numbers.push(numbers.length + 1);
	}
</script>

<p>{numbers.join(' + ')} = {total}</p>

<button onclick={addNumber}>
	Add a number
</button>

```

The expression inside the `$derived` declaration will be re-evaluated whenever its dependencies (in this case, just `numbers`) are updated. Unlike normal state, derived state is read-only.
每当 `$derived` 声明中的依赖项（在本例中，仅 `numbers`）更新时，都会重新评估 声明中的表达式。与普通状态不同，派生状态是只读的。