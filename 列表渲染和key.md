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
