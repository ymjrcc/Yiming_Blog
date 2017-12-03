---
title: learn-mobx
tags:
---

mobx 引入了几个概念，`Observable state`, `Derivations` 和 `Reactions`。

<!-- more -->

可以拿 Excel 表格做个比喻，`Observable state` 是单元格，`Derivations` 是计算公式，单元格的修改会触发公司的重新计算，并返回值，而最终公式的计算结果需要显示在屏幕上(比如通过图表的方式)，这是 `Reactions。`

通过 `@observable` 定义 `Observable state`，通过 `@computed` 定义 `Derivations`，通过 `@observer` 封装了 React Component 的 render 方法，这是 `Reactions。`

```js
import { observable, computed, autorun } from 'mobx';
import { observer } from 'mobx-react';
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

////////////////////
// Store

class TodoStore {
  @observable todos = [];

  constructor() {
    autorun(() => console.log(this.report));
  }

  @computed get report() {
    return `todos' length = ${this.todos.length}`;
  }    

  @computed get completedTodosCount() {
    return this.todos.filter(todo => todo.completed === true).length;
  }
  addTodo(task) {
    this.todos.push({ task, completed: false });
  }
}

////////////////////
// Components

@observer
class TodoList extends Component {
  render() {
    const { todoStore } = this.props;
    return (
      <div>
        { todoStore.todos.map((todo, index) => <Todo todo={todo} key={index} />) }
        Progress: { todoStore.completedTodosCount }
      </div>
    );
  }
}

@observer
class Todo extends Component {
  render() {
    const { todo } = this.props;
    return (
      <li onDoubleClick={this.onRename}>
        <input
          type="checkbox"
          checked={ todo.completed }
          onChange={ this.onToggleCompleted }
        />
        { todo.task }
      </li>
    );
  }
  onToggleCompleted = () => {
    const todo = this.props.todo;
    todo.completed = !todo.completed;
  }
  onRename = () => {
    const todo = this.props.todo;
    todo.task = prompt('Task name', todo.task) || ""; 
  }
}

////////////////////
// Init

const todoStore = new TodoStore();
todoStore.addTodo('foo');
todoStore.addTodo('bar');

ReactDOM.render(
  <TodoList todoStore={todoStore} />,
  document.getElementById('mount')
);
```

* `@observale` 修饰器让对象可以被追踪；
* `@computed` 修饰器创造了自动运算的表达式；
* `autorun` 函数让依靠 `observable` 的函数自动执行，这个用来写 log，发请求很不错；
* `@observer` 修饰器让 React 组件自动更新

参考资料：

* [MobX 官方文档](http://cn.mobx.js.org/)
* [MobX 入门教程 by sorycc](https://github.com/sorrycc/blog/issues/2)
* [使用mobx开发高性能react应用](http://www.reactpeixun.com/reactganhuo/2017-02-20/271.html)
* [我为什么从Redux迁移到了Mobx by 有赞](https://segmentfault.com/a/1190000012209750)
* [MobX 入门教程](http://blog.csdn.net/yelin042/article/details/75264637)
* [Mobx使用详解](http://www.jianshu.com/p/505d9d9fe36a)
* [MobX —— 10分钟极速入门 MobX 与 React](http://eyehere.net/2016/mobx-getting-started/)