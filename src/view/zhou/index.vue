<template>
    <div>
      <h1>TodoList</h1>
      <div>
        <Button type="primary" @click="createTodo">创建日程</Button>
        <br>
        <br>
        <Table border :columns="columns" :data="datas">
          <template slot-scope="{ row, index }" slot="time">
              <strong>{{ row.time }}</strong>
          </template>

          <template slot-scope="{ row, index }" slot="action">
              <Button type="primary" style="margin-right: 5px" @click="show(row)">View</Button>
              <Button type="primary" style="margin-right: 5px" @click="edit(row)">Edit</Button>
              <Button type="primary" @click="remove(row)">Delete</Button>
          </template>
        </Table>
      </div>
    </div>
</template>

<script>
import { getTodoList, deleteTodo } from '@/api/data'

export default {
  data () {
    return {
      columns: [
        {
          title: '时间',
          slot: 'time',
          sortable: true
        },
        {
          title: '事件',
          key: 'todothing'
        },
        {
          title: '操作',
          slot: 'action'
        }
      ],
      datas: [
        // {
        //   id: 1,
        //   time: '2016-10-02',
        //   todothing: '吃饭'
        // }
      ]
    }
  },
  methods: {
    getData () {
      // 显示todolist
      getTodoList().then(res => {
        console.log('请求成功，res =', res)
        var todos = res.data
        console.log('todos', todos)
        // 显示所有的todo
        for (let i = 0; i < todos.length; i++) {
          var todo = todos[i]
          var dataOfTodo = {
            id: todo.id,
            time: todo.time,
            todothing: todo.todothing
          }
          this.datas.push(dataOfTodo)
        }
      }).catch(err => {
        console.log('请求错误， err =', err)
      })
    },
    init () {
      this.getData()
    },
    show (row) {
      // 弹出对话框显示
      console.log('show on', row)
      this.$Modal.info({
        title: '日程事项',
        content: `
        时间：${row.time}
        事件：${row.todothing}
        `
      })
      console.log('this.$Modal.info = ', this.$Modal.info)
    },
    edit (row) {
      console.log('row', row)
    },
    remove (row) {
      /*
      删除一个item
      需要传一个id给后端，传的数据需要是一个字符串，所以需要格式转换
      后端去执行对应的删除功能
      */
      var itemId = row.id
      console.log('itemId', itemId)

      deleteTodo(itemId).then(res => {
        console.log('delect 成功')
        // 删除以后重新获取新的列表
        this.getData()
      })
    },
    createTodo () {
      console.log('跳转createlist界面')
      this.$router.push('createlist')
    }
  },
  mounted: function () {
    this.init()
  }
}
</script>
