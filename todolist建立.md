# 基于外部Vue.js库实现的一个文件的ToDoList功能页面

只需要一个html文件



以下是完整的HTML和JavaScript代码，用于创建一个基本的To do list前端页面，实现添加任务、切换任务状态和删除任务的功能，并且利用Vue动态绑定类名来改变已完成任务的样式。

### 完整的HTML和JavaScript代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To Do List</title>
    <style>
        *{
            font-family: 'Times New Roman', Times, serif;
        }
        body {
            font-family:'Times New Roman', Times, serif, sans-serif;
            margin: 100px;
            text-align: center;
        }

        .todo-item {
            font-size: 2vw;
            /* 按钮字体大小随视口宽度变化 */
            margin: 10px 0;
            padding: 6px;
            border: 1px solid #ddd;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #17fac9;
        }

        .todo-item.completed .task-content {
            background-color: #e6ffe6;
            text-decoration: line-through;
            text-decoration-color: #17fac9;
            transition: background-color 0.3s ease;
        }

        .todo-item.completed {
            background-color: #e6ffe6;
            /* 设置整个任务项的背景色 */
        }

        .task-content.completed {
            text-decoration: line-through;
            /* 设置任务内容的删除线 */
        }

        .add-task-input {
            width: 30vw;
            /* 输入框宽度随视口宽度变化 */
            padding: 1.5vh 2vw;
            /* 输入框内边距随视口高度和宽度变化 */
            margin-right: 1vw;
            /* 输入框右边距随视口宽度变化 */
            font-size: 2vw;
            /* 输入框字体大小随视口宽度变化 */
            margin-bottom: 3%;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }

        .add-task-btn {
            padding: 1.5vh 3vw;
            /* 按钮内边距随视口高度和宽度变化 */
            border-radius: 0.5vw;
            /* 按钮边框半径随视口宽度变化 */
            font-size: 2vw;
            /* 按钮字体大小随视口宽度变化 */
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .add-task-btn:hover {
            background-color: #45a049;
        }

        .task-buttons button {
            margin-left: 1vw;
            /* 按钮左边距随视口宽度变化 */
            padding: 1vh 2vw;
            /* 按钮内边距随视口高度和宽度变化 */
            border-radius: 0.5vw;
            /* 按钮边框半径随视口宽度变化 */
            font-size: 2vw;
            /* 按钮字体大小随视口宽度变化 */
            background-color: #f44336;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .task-buttons button:hover {
            background-color: #d32f2f;
        }

        h1 {
            font-size: 4vw;
            /* 标题字体大小随视口宽度变化 */
            text-align: center;
            margin-bottom: 20px;
            margin-top: 20px;
            color: #0dcf3a;
        }

        div {
            text-align: center;
            margin-top: 20px;
            font-size: 16px;
            color: #808080;

        }
    </style>
</head>

<body>
    <div id="app">
        <h1>To Do List</h1>
        <input type="text" v-model="newTask" class="add-task-input" placeholder="Add new task">
        <button @click="addTask" class="add-task-btn">Add Task</button>
        <div v-for="(task, index) in tasks" :key="task.id" class="todo-item" :class="{ 'completed': task.completed }">
            <span class="task-content" :class="{ 'completed': task.completed }">{{ task.content }}</span>
            <div class="task-buttons">
                <button @click="toggleTaskStatus(index)">Toggle</button>
                <button @click="removeTask(index)">Remove</button>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                newTask: '',
                tasks: []
            },
            methods: {
                addTask() {
                    if (this.newTask.trim() !== '') {
                        this.tasks.push({
                            id: Date.now(), // 使用时间戳作为id
                            content: this.newTask,
                            completed: false
                        });
                        this.newTask = ''; // 添加任务后清空输入框
                    }else{
                        alert('Task content cannot be empty!');
                    }
                },
                toggleTaskStatus(index) {
                    this.tasks[index].completed = !this.tasks[index].completed;
                },
                removeTask(index) {
                    this.tasks.splice(index, 1);
                }
            }
        });
    </script>
</body>

</html>
```

### 代码解释

1. **HTML结构**：
   - `<div id="app">`：Vue实例的挂载点。
   - `<input type="text" v-model="newTask" class="add-task-input" placeholder="Add new task">`：输入框，用于输入新的任务内容，通过`v-model`双向绑定到`newTask`数据属性。
   - `<button @click="addTask" class="add-task-btn">Add Task</button>`：按钮，点击时调用`addTask`方法添加新任务。
   - `<div v-for="(task, index) in tasks" :key="task.id" class="todo-item" :class="{ 'completed': task.completed }">`：使用`v-for`指令遍历`tasks`数组，为每个任务生成一个`<div>`，并通过`:class`动态绑定类名，根据`task.completed`的值决定是否添加`completed`类。
   - `<button @click="toggleTaskStatus(index)">Toggle</button>`：按钮，点击时调用`toggleTaskStatus`方法切换任务的完成状态。
   - `<button @click="removeTask(index)">Remove</button>`：按钮，点击时调用`removeTask`方法删除任务。

2. **CSS样式**：
   - `.todo-item`：任务项的基本样式。
   - `.todo-item.completed`：已完成任务的样式，背景色为浅绿色，文本有删除线。
   - `.add-task-input`：输入框的样式。
   - `.add-task-btn`：添加任务按钮的样式。
   - `.task-buttons button`：任务操作按钮的样式。

3. **JavaScript部分**：
   - `new Vue({ ... })`：创建一个新的Vue实例，挂载到`#app`元素上。
   
   - `data`：定义Vue实例的数据属性，包括`newTask`（新任务内容）和`tasks`（任务列表）。
   
   - `methods`：定义Vue实例的方法，包括`addTask`（添加任务）、`toggleTaskStatus`（切换任务状态）和`removeTask`（删除任务）。
   
   - `<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>`
   
     - 这是一个`<script>`标签，用于在网页中引入外部JavaScript文件。
     - `src`属性指定了要引入的JavaScript文件的URL。
     - `https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js`是一个CDN（内容分发网络）地址，它指向了Vue.js的2.6.14版本的文件。
     - 通过这种方式，可以直接在网页中使用Vue.js库，而无需将Vue.js的代码文件下载到本地项目中。CDN会根据用户的地理位置等因素，从离用户最近的服务器上提供文件，这样可以加快文件的加载速度。
   
     `<script src="app.js"></script>`
   
     - 这也是一个`<script>`标签，用于引入本地的JavaScript文件。
     - `src`属性的值是`app.js`，表示该文件位于当前HTML文件所在目录下的`app.js`文件。
     - `app.js`文件通常是我们自己编写的JavaScript代码文件，用于实现网页的特定功能。在前面的To do list示例中，`app.js`文件包含了使用Vue.js创建To do list应用的JavaScript代码，比如定义Vue实例、数据和方法等。
   
     功能总结：
   
     1. 从CDN引入Vue.js库，以便在网页中使用Vue.js的功能。
     2. 引入本地的`app.js`文件，该文件包含了使用Vue.js实现To do list应用的具体代码。

将上述代码保存为一个HTML文件，然后在浏览器中打开，即可看到一个基本的To do list应用。

