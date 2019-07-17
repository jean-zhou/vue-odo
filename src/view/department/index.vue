<template>
    <div>
        <div>
            <Button type="success" @click="createDepartment">Create</Button>
            <br>
            <br>
        </div>

        <Table :columns="columns" :data="data">
            <template slot-scope="{ row, index }" slot="id">
                <span>{{ row.id}}</span>
            </template>

            <template slot-scope="{ row, index }" slot="name">
                <span>{{ row.name}}</span>
            </template>

            <template slot-scope="{ row, index }" slot="action">
                <Button type="primary" @click="deleteDepartment(row)">删除</Button>
                <Button type="warning" @click="editDepartment(row)">编辑</Button>
            </template>
        </Table>
    </div>
</template>

<script>
    import {getEmployeeData} from '@/api/data'
    import {deleteEmployeeData} from '@/api/data'


    export default {
        data() {
            return {
                columns: [
                    {
                        title: '部门编号',
                        slot: 'id'
                    },
                    {
                        title: '部门名称',
                        slot: 'name'
                    },
                    {
                        title: '操作',
                        slot: 'action'
                    }
                ],

                data: [
                    {
                        id: '王小明',
                        name: 18,
                        birthday: '919526400000',
                        address: '北京市朝阳区芍药居'
                    },
                    {
                        id: '张小刚',
                        name: 25,
                        birthday: '696096000000',
                        address: '北京市海淀区西二旗'
                    },
                ],
                editIndex: -1,  // 当前聚焦的输入框的行数
                editName: '',  // 第一列输入框，当然聚焦的输入框的输入内容，与 data 分离避免重构的闪烁
                editAge: '',  // 第二列输入框
                editBirthday: '',  // 第三列输入框
                editAddress: '',  // 第四列输入框
            }
        },
        methods: {
            deleteData() {
                console.log("点击了删除。。。第一次测试")
            },
            getList: function () {
                getEmployeeData().then(res => {
                    console.log("list func 执行成功")
                    var datas = res.data.body.items
                    console.log("res:", res.body, res.data)
                    console.log(datas)
                    this.data = datas
                    console.log('2333333333333333333333333')
                }).catch(err => {
                    console.log("getEmployeeData  Ajax 函数报错了")
                    console.log(err)
                })
            },

            init() {
                this.getList()
            },

            createDepartment() {
                // 里面填路径
                this.$router.push("department_create")

            },


            editDepartment(row) {
                console.log("row:", row)
                var path = "department_edit" + '/?id=' + row.id
                this.$router.push(path)

            },

            deleteDepartment(row) {

                console.log("testing******", row.id)

                var json_id = {
                    ids: [row.id]
                }

                json_id = JSON.stringify(json_id)
                console.log('json_id', typeof (json_id), json_id)

                deleteEmployeeData(json_id).then(res => {
                    console.log("delete department func success")
                    this.getList()
                }).catch(err => {
                    console.log("deleteEmployeeData  Ajax 函数报错了")
                    console.log(err)
                })
            }

        },
        mounted: function () {
            this.init();
        }
    }


</script>
