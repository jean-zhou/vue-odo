<template>
  <div>
    <div>
      <Button type="primary" @click="createTodo">创建日程</Button>
      <br><br>
    </div>
      <Button type="primary" icon="ios-search">搜索日程</Button>
      <br><br>
    <div>
      <Table border :columns="columns" :data="data">
        <!-- 首行加粗，使用插槽对于输入的内容加粗
            插槽的内容由父组件传给他
            使用template 作为标签，表示这个是一组件，子组件
         -->
        <template slot-scope="{ row, index }" slot="time">
            <strong>{{ row.time }}</strong>
        </template>
        <!-- 是一个组件
          目的：给表格最后添加两个按钮
          使用：使用插槽插入按键
         -->
        <template slot-scope="{ row, index }" slot="action">
            <Button type="primary" size="small" style="margin-right: 5px" @click="show(index)">View</Button>
            <Button type="error" size="small" style="margin-right: 5px" @click="edit(index)">Edit</Button>
            <Button type="error" size="small" @click="remove(index)">Delete</Button>
        </template>
      </Table>
    </div>
  </div>
</template>

<script>
import { getTodoList, delectTodo } from '@/api/data'

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
      data: [
        {
          id: 1,
          time: '2016-10-02',
          todothing: '吃饭'
        }
      ]
    }
  },
  methods: {
    // 刷新以后获取todo，插入到data中
    // .then,是给在api中定义好的getTodoList()添加一个回调函数的方法
    // 这个then方法已经封装了一个ajax的回调，需要一个函数参数，
    // 传入的函数参数是一个箭头函数
    getList () {
      getTodoList().then(res => {
        console.log('请求成功，res =', res)
      })
    },
    init () {
      this.getList()
    },
    show (index) {
      /*
         show cal
      */
      this.$Modal.info({
        title: '日程事项',
        content: `时间：${this.data[index].time}<br>
                  事件：${this.data[index].todothing}<br>`
      })
    },
    createTodo () {
      /*
         跳转创建todo界面
      */
      console.log('跳转createtodo界面')
      this.$router.push('createtodo')
    },

    // 跳转到编辑界面
    edit (index) {
      console.log('跳转createtodo界面')
      this.$router.push('edittodo')
    },
    // 删除该行
    // 此方法是使用的template的组件上，这个组件是操作这一行的数据
    // 所以它的删除也是index
    // 界面上的js的splice用法，是用来添加或者删除数据的
    // 后台数据的删除，
    // 在萧的ajax中删除数据，就是传需要删除的事项的id给后台，事项删除了以后，把剩下的数据返回重新渲染
    remove (index) {
      // 界面数据的删除
      var json_id = {
        ids: index
      }
      console.log('index', json_id)
      json_id = JSON.stringify(json_id)

      delectTodo(json_id).then(res => {
        this.getList()
        // 显示界面的删除
        this.data.splice(index, 1)
      }).catch(err => {
        console.log(err)
      })
    }
  },
  // 使用生命周期，在组件一挂载，就调用此方法
  // 是什么组件？App组件？
  // 如何使用，就直接使用this.来调用已经写好的函数，this代表这个vue对象，对象在哪？--看下原码
  mounted () {
    this.init()
  }
}
</script>
