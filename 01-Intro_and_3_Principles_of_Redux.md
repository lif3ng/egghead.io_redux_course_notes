# 01. 单向不可变状态树
[Video Link](https://egghead.io/lessons/javascript-redux-the-single-immutable-state-tree?series=getting-started-with-redux)

Redux 的第一原则 (无论有多复杂):

**应用的整体状态将由一个 JS 对象来表示。**

对于应用的所有改变都是明确的。
这些变化，无论是数据还是UI的状态，都被包含在一个叫做 **state** 的单一对象中。

因为全部状态都有一个对象来表示，所以我们可以跟踪不同时间的变化。

# 02. 通过 Action 描述状态改变
[Video Link](https://egghead.io/lessons/javascript-redux-describing-state-changes-with-actions?series=getting-started-with-redux)

Redux 的第二原则是 ** *状态树* 只读**。
任何时候你想要改变状态，你必须分发一个 **action** 。action 是一个描述状态改变的纯JS对象。就像 state 是数据的最简表示一样，action 是数据变化的最简表示。

action 的唯一要求是拥有 type 属性（通常是一个字符串）。

比如，在计数器应用中，有 `INCREMENT` 和 `DECREMENT` actions， 对于 ToDo 应用，展示组件不知道一个条目如何被加到列表中--它们只知道 `ADD_TODO` action 被分发，这个 action 拥有 `text` 内容 和 `id` 序号。 

总体原则是 state 是只读的， 只能通过分发 action 被改变。

# 03. Pure and Impure Functions
[Video Link](https://egghead.io/lessons/javascript-redux-pure-and-impure-functions)

Before learning more about Redux, it's important to know the difference between "Pure" and "Impure" functions.

**Pure:**
```JavaScript
function square(x) {
  return x * x;
}
function squareAll(items) {
  return items.map(square);
}
```
Pure functions are those whose return values depend only upon the values of their arguments. Pure functions don't have side effects like network or database calls. Pure functions also do not override the values of anything. In the above example, a new array is returned instead of modifying the `items` that was passed in.

**Impure:**
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
Contrast the "Impure" function. A database is called, and values passed in are being overwritten.

This distinction is important to understand, since Redux requires that certain functions are pure.

# 04. The Reducer Function
[Video Link](https://egghead.io/lessons/javascript-redux-the-reducer-function)

React introduced the idea that the UI layer is most predictable when it is described as a pure function of the application's state.

Redux complements this approach by requiring that state mutations in your app need to be described by a pure function that takes the previous state and the action being dispatched, and returns the next state of your application.

**Inside a Redux application there is one particular function that takes the previous state and the action being dispatched, and returns the next state of the whole application**. It is important that the function is pure (i.e. the state being given to it isn't modified) because it has to return the new object representing the application's new state.

Even in large applications, there is still just a single function that calculates the new state of the application. It doesn't have to be slow-- if certain parts of the state haven't changed, their references can stay as-is. In the ToDo app example, when changing the visibility between "All/Completed/Active" the actual items themselves haven't changed, so the reference to the previous version of the `todos` array is left intact.

This is the 3rd and final principle of Redux: to describe state mutations you have to write a function that takes the previous state of the app and the action being dispatched, then returns the next state of the app. This function is called the **Reducer**.


<p align="center">
<a href="./02-Reducer_and_Store.md">Next -></a>
</p>
