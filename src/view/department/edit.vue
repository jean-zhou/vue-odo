<template>
    <div>
        <br><br>
        <Input v-model="name" placeholder="请输入部门名称" style="width: 300px"/>
        <br>
        <Input v-model="description" placeholder="请输入部门描述" style="width: 300px"/>
        <br>
        <div class="vbnt">
            <Button type="info" @click="backHandler">返回</Button>
            <Button type="success" @click="editHandler">提交</Button>
        </div>

    </div>
</template>

<script>


    import {editEmployeeData} from '@/api/data'
    import {detailEmployeeData} from '@/api/data'

    export default {
        data() {
            return {
                name: '',
                description: '',
            }
        },

        methods: {

            getDetail: function () {
                var json_id = {
                    id: this.$route.query.id
                }

                var department = JSON.stringify(json_id)

                detailEmployeeData(department).then(res => {
                    console.log("detail data function success")
                    console.log("detail testing******", res)
                    this.name = res.data.body.user.name
                    this.description = res.data.body.user.description
                }).catch(err => {
                    console.log("detailEmployeeData  Ajax 函数报错了")
                    console.log(err)
                })

            },

            init() {
                this.getDetail()
            },

            editHandler: function () {
                console.log('按钮被点击到了************')
                console.log(this.$route.query.id)
                var o = {

                    // 思考这个 id 怎么拿到 ？？？
                    id: this.$route.query.id,
                    description: this.description,
                    name: this.name,
                }

                var department = JSON.stringify(o)


                editEmployeeData(department).then(res => {
                    //this.tableData = res.data
                    console.log("create data function success")
                    this.$router.back()
                }).catch(err => {
                    console.log("getEmployeeData  Ajax 函数报错了")
                    console.log(err)
                })
            },

            backHandler() {
                this.$router.back()
            }
        },


        mounted: function () {
            this.init()
        }
    }
</script>

<style>
    Button {
        margin-left: 30px;
        position: relative;
        right: 30px;
    }

    Input {
        margin-bottom: 10px;
    }

    .vbnt {
        position: relative;
        right: -153px;
    }
</style>
