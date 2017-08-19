# 01. 单一不可变状态树
[Video Link](https://egghead.io/lessons/javascript-redux-the-single-immutable-state-tree?series=getting-started-with-redux)

Redux 的第一原则 (无论有多复杂):

**应用的整体状态将由一个 JS 对象来表示。**

对于应用的所有改变都是明确的。这些变化，无论是数据还是UI的状态，都被包含在一个叫做 **state** 的单一对象中。

因为全部状态都有一个对象来表示，所以我们可以跟踪不同时间的变化。

# 02. 通过 Action 描述状态改变
[Video Link](https://egghead.io/lessons/javascript-redux-describing-state-changes-with-actions?series=getting-started-with-redux)

Redux 的第二原则是 ** *状态树* 只读**。
任何时候你想要改变状态，你必须分发一个 **action** 。action 是一个描述状态改变的纯JS对象。就像 state 是数据的最简表示一样，action 是数据变化的最简表示。

action 的唯一要求是拥有 type 属性（通常是一个字符串）。

比如，在计数器应用中，有 `INCREMENT` 和 `DECREMENT` actions， 对于 ToDo 应用，展示组件不知道一个条目如何被加到列表中--它们只知道 `ADD_TODO` action 被分发，这个 action 拥有 `text` 内容 和 `id` 序号。 

总体原则是 state 是只读的， 只能通过分发 action 被改变。

# 03. 纯方法和非纯方法
[Video Link](https://egghead.io/lessons/javascript-redux-pure-and-impure-functions)

在学习更多 Redux 知识之前，弄清楚“纯方法”和“非纯方法”之间的区别是很重要的。

**纯函数:**
```JavaScript
function square(x) {
  return x * x;
}
function squareAll(items) {
  return items.map(square);
}
```
纯方法的返回值只由传入参数的值决定。纯方法不会操作网络或者数据库。纯方法也不会覆盖任何值。在上面的例子中，返回了一个新数组，而不是修改传入的 `items`。

**非纯函数:**
```JavaScript
function square(x) {
  updateXInDatabase(x);
  return x * x;
}
function squareAll(items) {
  for (let i = 0; i < items.length; i++) {
    items[i] = square(items[i]);
  }
}
```
对比“非纯”函数，调用了数据库，传入的值被覆盖了。

这一差别对于理解很重要，因为 Redux 要求某些方法是纯方法。

# 04. Reducer 方法
[Video Link](https://egghead.io/lessons/javascript-redux-the-reducer-function)

React 引入了这样一个概念：使用纯方法描述应用状态时，UI 层最可预测的。

Redux 补充了这种方法：应用中的状态改变通过一个纯函数来描述，这个函数通过先前的状态和一个被分发的action， 返回应用的下一个状态。

**Inside a Redux application there is one particular function that takes the previous state and the action being dispatched, and returns the next state of the whole application**. It is important that the function is pure (i.e. the state being given to it isn't modified) because it has to return the new object representing the application's new state.

Even in large applications, there is still just a single function that calculates the new state of the application. It doesn't have to be slow-- if certain parts of the state haven't changed, their references can stay as-is. In the ToDo app example, when changing the visibility between "All/Completed/Active" the actual items themselves haven't changed, so the reference to the previous version of the `todos` array is left intact.

This is the 3rd and final principle of Redux: to describe state mutations you have to write a function that takes the previous state of the app and the action being dispatched, then returns the next state of the app. This function is called the **Reducer**.


<p align="center">
<a href="./02-Reducer_and_Store.md">Next -></a>
</p>
