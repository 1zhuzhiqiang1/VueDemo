# Vue.js

## Vue实例

#### Vue.js 选项对象
1. https://cn.vuejs.org/v2/api/#data 
2. 只有当 vue 实例被创建的时候，data的数据才是响应式的
3. 使用 `Object.freeze()` 可以阻止修改现有的属性，也就意味着将不是响应式的

### vue 暴露了一些有用的属性和方法
1. https://cn.vuejs.org/v2/api/#%E5%AE%9E%E4%BE%8B%E5%B1%9E%E6%80%A7

### 生命周期钩子
1. 作用: 给用户在不同的阶段添加自己的代码的机会
2. 注意事项： 不要在选项属性或者回调中使用箭头函数 () => {}, 因为箭头函数是和父级上下文绑定在一起的，this不会是如你所预期的Vue实例
3. https://cn.vuejs.org/v2/guide/instance.html#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%E7%A4%BA

## 模板语法
Vue.js使用了基于 html 的模板语法。 在底层实现上，Vue 将模板编译成虚拟DOM渲染函数。

### 插值
1. 通过 `v-once` 指令，执行一次性的插值。当数据改变时，插值处的内容也不会更新
2. `v-html` 指令，输出原始的 HTML。 警告: 绝不要对用户提供的内容使用 v-html 插值

#### 特性
1. Mustache 语法不能作用在 HTML 特性上，遇到这种情况应该使用 `v-bind` 指令

#### JavaScript 表达式
1. 每个绑定都只能包含<b>单个</b>表达式

###指令
1. `v-if` `v-for` `v-bind` `v-on` 
2. 一个指令可以接受一个参数，在指令名称之后用 `:` 表示 
3. 修饰符
4. 缩写 `v-bind` > `:`    `v-on`>`@`

## 计算属性和侦听器
### 计算属性
对于任何复杂逻辑，你都应当使用计算属性。 computed
1. 计算属性是基于依赖进行缓存数据的
2. 计算属性默认只有 getter, 但是也可以提供一个 setter

### 侦听器
watch
计算属性在大多数情况下合适，但是也有不满足情况的例子，这个时候我们就需要使用 watch 属性来做。
比如我们需要在数据发生变化时，去后台请求数据

## Class 与 Style 绑定
操作元素的 class 列表和内联样式是数据绑定的一个常见需求，我们可以用 v-bind 处理它们：只需要通过表达式计算出字符串结果即可。
表达式结果的类型除了字符串之外，还可以是对象或数组。

### 绑定 HTML class

#### 对象语法

```

<div v-bind:class="{ active: isActive }"></div>

<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>

data: {
  isActive: true,
  hasError: false
}

```


绑定的数据对象不必内联定义在模板里：

``` 

<div v-bind:class="classObject"></div> 

data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}

```

<big>我们也可以在这里绑定一个返回对象的计算属性</big>

```
<div v-bind:class="classObject"></div>

data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}

```

#### 数组语法

```
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

<div v-bind:class="[activeClass, errorClass]"></div>

<div v-bind:class="[{ active: isActive }, errorClass]"></div>

```

