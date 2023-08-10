# vue 编码规范

## 组件命名

1. 组件名为多个单词，命名为组件用途，完整单词的组件名（倾向于完整单词而不是缩写）
2. 文件名应该要么始终是单词大写开头 (PascalCase)，要么始终是横线连接 (kebab-case)，例如：todo-item或TodoItem
3. 基础组件名, 应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，比如Base、App或V
4. 紧密耦合的组件名, 和父组件紧密耦合的子组件应该以父组件名作为前缀命名

```typescript
// bad
export default {
  name: 'Todo',
  // ...
}

// good
export default {
  name: 'TodoItem',
  // ...
}
```

## 模板中的组件名大小写

推荐都使用 kebab-case

```vue
// good
<my-component />
```



## **组件的 `data` 必须是一个函数。**

当在组件中使用 `data` property 的时候 (除了 `new Vue` 外的任何地方)，它的值必须是返回一个对象的函数。

```typescript
// bad
export default {
  data: {
    foo: 'bar'
  }
}

// good
export default {
  data () {
    return {
      foo: 'bar'
    }
  }
}

// 在一个 Vue 的根实例上直接使用对象是可以的，
// 因为只存在一个这样的实例。
new Vue({
  data: {
    foo: 'bar'
  }
})
```

## Prop 定义应该尽量详细

在你提交的代码中，prop 的定义应该尽量详细，至少需要指定其类型。

> 细致的 **prop** 定义有两个好处：
>
> - 它们写明了组件的 API，所以很容易看懂组件的用法；
> - 在开发环境下，如果向一个组件提供格式不正确的 prop，Vue 将会告警，以帮助你捕获潜在的错误来源

```typescript
// bad
props: ['status']

// good
props: {
  status: String
}
// 更好的做法！
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}

```



## 为 `v-for` 设置键值

**总是用 `key` 配合 `v-for`。**

1. 为v-for设置键值，尽量避免使用index作为key 
2. 在vue2版本中，避免v-if和v-for用在一起

```vue
// bad
<ul>
  <li v-for="todo in todos">
    {{ todo.text }}
  </li>
</ul>

// good
<ul>
  <li
    v-for="todo in todos"
    :key="todo.id"
  >
    {{ todo.text }}
  </li>
</ul>

```

## 样式

为组件样式设置作用域，使用scoped属性，使用BEM约定

## 私有property名

*推荐使用$* 前缀，作为一个用户定义的私有property的约定，以确保不会和Vue自身相冲突

## 自闭合组件

在单文件组件、字符串模板和 JSX 中没有内容的组件应该是自闭合的——但在 DOM 模板里永远不要这样做。

## 多个 attribute 的元素

1.  多个attribute的元素应该分多行撰写，每个attribute一行 
2. 带引号的attribute值

```vue
// bad
<img src="https://vuejs.org/images/logo.png" alt="Vue Logo">
<my-component foo="a" bar="b" baz="c"/>

// good
<img
  src="https://vuejs.org/images/logo.png"
  alt="Vue Logo"
>
<my-component
  foo="a"
  bar="b"
  baz="c"
/>

```

## 模板中简单的表达式

组件模板应该只包含简单的表达式，复杂的表达式则应该重构为计算属性或方法

## 简单的计算属性

应该把复杂计算属性分割为尽可能多的更简单的property，计算属性不能产生副作用

## 指令

使用指令缩写 (用 : 表示 v-bind:、用 @ 表示 v-on: 和用#表示 v-slot:)，应该要么都用要么都不用。

## 组件通信

应该优先通过prop和事件进行父子组件之间的通信

## 事件、定时器

清除定时器或者事件监听

## 代码文件

开发过程中单个文件长度尽量控制**600**行以内，特别复杂的功能，文件不允许超过**1000**行

