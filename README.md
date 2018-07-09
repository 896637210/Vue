# Vue
注意点

###vue实例
#### Object.freeze()，这会阻止修改现有的属性，也意味着响应系统无法再追踪变化。
```var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})```
#### Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。
```
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 这个回调将在 `vm.a` 改变后调用
})
```
#### 实例生命周期钩子
##### 数据监听、编译模版、实例挂载到DOM并在数据变化时更新DOM等，同时这个过程运行一些叫做生命周期钩子的函数
##### created钩子会在实例被创立之后执行代码（mounted挂载dated、destroyed销毁）
```
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```
