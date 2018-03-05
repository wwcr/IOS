<!--页面css样式-->
<style scoped>
    .firm input {
        width: 100%;
        height: 1.4rem;
        color: #666;
        background: #fff;
        font-size: 0.4rem;
        text-indent: 0.4rem;
    }
    .right_btn{
        font-size: 0.4rem;
        color: #ffffff;
        height: 1.25rem;
        line-height: 1.25rem;
    }
</style>
<!--企业名称-->
<template>
    <div>
        <div class="header">
            <a href="javascript:history.go(-1);" class="go_return"></a>
            <p class="title">昵称</p>
            <a class="right_btn" @click="save()">
                保存
            </a>
        </div>
        <div class="firm">
            <input v-model="name" type="text" placeholder="请输入昵称"/>
        </div>
    </div>
</template>
<script type="text/javascript">
    import units from '../../tools/units'
    import lrz from '../../../static/lrz/lrz.bundle'
    import cookie from '../../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                thumb: '',
                info: {},
                name:''
            }
        },
        methods: {
            save:function () {
                layer.loading('请稍等...');
                let that= this;
                new Promise(function () {
                    that.Http('user/changeNickname',{
                        name:that.name
                    },function (res) {
                        layer.loading(false);
                        layer.msg(res.msg,2,function () {
                            if(res.code > 0){
                                history.go(-1)
                            }
                        })
                    })
                })
            }
        },
        created: function () {
            this.name = this.$route.query.t;
            units.title.set('设置昵称');
        }
    }
</script>