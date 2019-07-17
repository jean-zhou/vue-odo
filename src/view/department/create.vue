<template>
<div>
<br><br>
    <Input v-model="name" placeholder="请输入部门名称" style="width: 300px"  />
    <br>
    <br>

    <Input v-model="description" placeholder="请输入部门描述" style="width: 300px" />
    <br><br>

    <Button type="success" @click="createHandler">提交</Button>

</div>
</template>

<script>


	import { createEmployeeData } from '@/api/data'
    export default {
        data () {
            return {
                name: '',
                description: '',
            }
        },
      
        methods:{
            createHandler: function(){
                console.log('按钮被点击到了************')
                
                var o = {
                    name: this.name,
                    description: this.description
                }
                
                var department = JSON.stringify(o)

                
                
				createEmployeeData(department).then(res => {
					//this.tableData = res.data
                    console.log("create data function success")
                    this.$router.back()
				}).catch(err => {
					console.log("getEmployeeData  Ajax 函数报错了")
  					console.log(err)
				})


            }
        }
    }
</script>
