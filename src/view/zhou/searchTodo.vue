<template>
    <div>
      <h1>searchTodo</h1>
      <Table border :columns="columns" :data="data"></Table>
    </div>
</template>

<script>
import { getTodoList } from '@/api/data'

export default { 
  data () {
    return {
      columns: [
        {
          title: '时间',
          key: 'time'
        },
        {
          title: '事件',
          key: 'todothing'
        },
        {
          title: '操作',
          key: 'action'
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
    getData () {
      getTodoList().then(res => {
        console.log('请求成功，res =', res)
      }).catch(err => {
        console.log('请求错误， err =', err)
      })
    },
    init () {
      this.getData()
    }
  },
  mounted: function (){
    this.init()
  }
}
</script>
