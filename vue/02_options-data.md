### 问题： Vue组件data选项为什么必须是个函数而Vue的根实例则没有此限制？
因为同个组件生成多个实例的情况，每个实例用的组件选项对象是同一个，所以每个实例的this.$options.data指向的都是同一个地址。这时候data选项是对象的话多个实例共用会互相影响。所以需要使用函数，每个新创建的实例各自调用一下data选项的函数，返回一个全新的对象。

如下，_data为最终要进行响应式的data对象
```js
vm._data = typeof vm.$options.data === 'function'
    ? vm.$options.data.call(vm, vm)
    : data
```