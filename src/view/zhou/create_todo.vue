<template>
    <div>
      <h1>creactTodo</h1>
      <div>
        <template>
        <Form>
          <FormItem label="id">
            <Input v-model="formItem.id" style="width: 300px" />
          </FormItem>
          <FormItem label="日期">
            <Input v-model="formItem.time" style="width: 300px" />
          </FormItem>
          <FormItem label="事项">
            <Input v-model="formItem.todothing" style="width: 300px" />
          </FormItem>
        </Form>
      </template>
      </div>
      <div>
        <Button type="primary" @click="todoback">创建</Button>
      </div>
    </div>
</template>

<script>
import { saveTodo } from '@/api/data'
export default {
  data () {
    return {
      formItem: {
        id: '',
        time: '',
        todothing: ''
      }
    }
  },
  methods: {
    todoback () {
      var todo = JSON.stringify(this.formItem)
      console.log('todo', todo)

      saveTodo(todo).then(res => {
        console.log('请求成功, res', res.data)
      })
    }
  }
}
</script>
