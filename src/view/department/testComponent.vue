<testComponent>
    <div>
        <Input v-model="value" placeholder="Enter something..." style="width: 300px" />
        <Input v-model="value" placeholder="Enter something..." style="width: 300px" />
    </div>
</testComponent>
<script>
    export default {
        data () {
            return {
                value: ''
            }
        }
    }
</script>
