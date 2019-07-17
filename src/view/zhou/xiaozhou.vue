<template>
    <div>
      <h1>first demo testing</h1>
      <h1 v-for='item in msg'>{{item.id}}={{item.name}}</h1>
      <Button type="success" @click="buttonHandler">Success</Button>
      <Table border :columns="columns1" :data="data1">
            <template slot-scope="{ row, index }" slot="name">
                <span>{{ row.name}}</span>
            </template>

            <template slot-scope="{ row, index }" slot="age">
                <span>{{ row.age}}</span>
            </template>

            <template slot-scope="{ row, index }" slot="address">
                <span>{{ row.address}}</span>
            </template>

            <template slot-scope="{ row, index }" slot="action">
                <Button class='btn' type="success" >删除</Button>
                <Button class='btn' type="info" >编辑</Button>
            </template>
      </Table>
      
    </div>
</template>

<script>
export default {
  name: 'directive_page',
  data () {
    return {
        columns1: [
              {
                  title: 'Name',
                  slot: 'name'
              },
              {
                  title: 'Age',
                  slot: 'age'
              },
              {
                  title: 'Address',
                  slot: 'address'
              },
              {
                  title: 'Action',
                  slot: 'action'
              }
          ],
          data1: [
              {
                  name: 'John Brown',
                  age: 18,
                  address: 'New York No. 1 Lake Park',
                  date: '2016-10-03'
              },
              {
                  name: 'Jim Green',
                  age: 24,
                  address: 'London No. 1 Lake Park',
                  date: '2016-10-01'
              },
              {
                  name: 'Joe Black',
                  age: 30,
                  address: 'Sydney No. 1 Lake Park',
                  date: '2016-10-02'
              },
              {
                  name: 'Jon Snow',
                  age: 26,
                  address: 'Ottawa No. 2 Lake Park',
                  date: '2016-10-04'
              }
          ],
        msg: [
                {
                  id: '1',
                  name: 'jon',
                },
                {
                  id:'2',
                  name:'jim',
                }

             ]
          }
  },
  computed: {
    
  },
  methods: {
    showModal () {
      this.modalVisible = true
    },
    buttonHandler(){
      console.log('------ ')
    }
  }
}
</script>

<style>
.btn {
  margin-left: 4px;
}
</style>
