<template>
    <div class="content">
        <div class="list">
            {{content.content}}
        </div>
        <div class="time">
            {{dates(content.date)}}
        </div>
        <!-- <navcate></navcate> -->
    </div>
</template>
<style scoped>
	.list{
        font-size:0.4rem;
        padding: 2rem;
    }
    .time{
        font-size:0.4rem;
        text-align: right;
        width: 100%;
        padding-right: 1rem;
        color: #dddddd;
    }
</style>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    export default {
        name: 'content',
        data () {
            return {
                info: {},
                content:''
            }
        },
        components: {
            navcate
        },
        methods: {
            getdata: function () {
                let that = this;
                this.Http('message/content',{
                    id:that.$route.query.id
                },function (res) {
                    console.log(res);
                })
            },
            dates:function (t) {
                return units.formatDateTime(t*1000)
            }
        },
        created: function () {
            this.getdata();
            try{
                this.content = JSON.parse(this.$route.query.c);
                //units.title.set(this.content.title);
            }catch(e){}
            console.log(this.content);
        },
        beforeCreate: function () {
            units.title.set('消息详情');
        },
    }
</script>