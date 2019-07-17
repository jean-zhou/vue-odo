<template>
    <div>
      <h1>creactTodo</h1>
      <div>
        <template>
        <Form>
          <FormItem label="日期">
            <Input v-model="formItem.time" style="width: 300px" />
          </FormItem>
          <FormItem label="事项">
            <Input v-model="formItem.thing" style="width: 300px" />
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
  data() {
    return {
      formItem: {
        time: '',
        thing: ''
      }
    }
  },
  //  发送请求post，上传数据
  methods: {
    /*
    2.创建界面
    1）input的值需要发给后台
    2）点击创建按键，数据发送成功后，需要提示成功，同时跳转到todoList界面 —— todoList界面需要同步显示更新以后的数据【需要使用vue的数据驱动视图】
  */
    todoback() {
      console.log('todoList')

      // 上传数据
      // 把vue的中的数据赋值给todo，这一个组件的数据是绑定在formItem中，所以需要this.formItem获取
      var todoData = {
        time: this.formItem.time,
        thing: this.formItem.thing 
      }
      // 需要转换格式
      var todo = JSON.stringify(todoData)

      // 发送请求
      saveTodo(todo).then(res => {
        console.log('发送成功')
        this.$Message.info('保存成功')
        this.$router.back()
      }).catch(err => {
        console.log('发送错误', err)
      })
    }
  }
}
</script>