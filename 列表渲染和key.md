### vue v-for
```
<div v-for="(value, key, index) in object :key="item.id"">
  {{ index }}. {{ key }}: {{ value }}
</div>
  data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
```
 key 唯一性保证不就地复用

#### filter(), concat() 和 slice() 返回新的数组
```
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```
#### 注意事项
  * 当你利用索引直接设置一个项时，例如：vm.items[indexOfItem] = newValue
  * 当你修改数组的长度时，例如：vm.items.length = newLength
  ```
  var vm = new Vue({
  data: {
    items: ['a', 'b', 'c']
  }
})
vm.items[1] = 'x' // 不是响应性的
vm.items.length = 2 // 不是响应性的
  ```
  ***
  ```
  //1 Vue.set
Vue.set(vm.items, indexOfItem, newValue)
// 1Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)
// 2
vm.items.splice(newLength)
  ```
 #### 对于已经创建的实例，Vue 不能动态添加根级别的响应式属性。但是，可以使用 Vue.set(object, key, value) 有时你可能需要为已有对象赋予多个新属性，比如使用 Object.assign() 或 _.extend()。
 ```
 vm.userProfile = Object.assign({}, vm.userProfile, {
  age: 27,
  favoriteColor: 'Vue Green'
})
 ```
 
 #### 重要的例子
 ```
 <div id="todo-list-example">
  <form v-on:submit.prevent="addNewTodo">
    <label for="new-todo">Add a todo</label>
    <input
      v-model="newTodoText"
      id="new-todo"
      placeholder="E.g. Feed the cat"
    >
    <button>Add</button>
  </form>
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      v-bind:key="todo.id"
      v-bind:title="todo.title"
      v-on:remove="todos.splice(index, 1)"
    ></li>
  </ul>
</div>
 Vue.component('todo-item', {
  template: '\
    <li>\
      {{ title }}\
      <button v-on:click="$emit(\'remove\')">Remove</button>\
    </li>\
  ',
  props: ['title']
})

new Vue({
  el: '#todo-list-example',
  data: {
    newTodoText: '',
    todos: [
      {
        id: 1,
        title: 'Do the dishes',
      },
      {
        id: 2,
        title: 'Take out the trash',
      },
      {
        id: 3,
        title: 'Mow the lawn'
      }
    ],
    nextTodoId: 4
  },
  methods: {
    addNewTodo: function () {
      this.todos.push({
        id: this.nextTodoId++,
        title: this.newTodoText
      })
      this.newTodoText = ''
    }
  }
})
 ```
  
