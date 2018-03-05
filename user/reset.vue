<style scoped>
    .pass h6 {
        text-align: center;
        margin-top: 2%;
        font-weight: normal;
        font-size: 0.4rem;
    }

    .list {
        padding: 0 0;
    }

    .tel {
        margin-top: 0%;
        font-size: 0.38rem;
        line-height: 0.38rem;
        color: #666666;
        border-bottom: 1px solid #f1f1f1;
        height: 1.53rem;
        width: 100%;
    }

    .tel input {
        display: block;
        height: 1.5rem;
        width: 100%;
        /*line-height: 1.5rem;*/
        padding-left: 0.5rem;
    }

    .yzm {
        border-bottom: 1px solid #f1f1f1;
        font-size: 0.38rem;
        line-height: 0.38rem;
        color: #666666;
        height: 1.53rem;
        width: 100%;
        background: #fff;
    }

    .yzm input {
        width: 75%;
        height: 1.5rem;
        line-height: 1.5rem;
        padding-left: 0.5rem;
        float: left;
    }

    .yzm a {
        width: 25%;
        height: 1.5rem;
        display: inline-block;
        line-height: 1.5rem;
        color: #2c7dfe;
        font-size: 0.26rem;
    }

    .sub_next {
        padding: 0.58rem 0.75rem 0.63rem;
        background: #fff;
    }

    .sub_next a {
        display: block;
        background: #377bee;
        color: #fff;
        text-align: center;
        line-height: 1.3rem;
        font-size: 0.52rem;
        border-radius: 0.1rem;
    }

    .sub_next a.gray {
        background: #377bee;
    }
</style>
<!--找回密码-->
<template>
    <div class="pass">
        <div class="list">
            <div class="tel">
                <input type="tel" v-model="oldpwd" placeholder="请输入原密码"/>
            </div>
            <div class="tel">
                <input type="password" v-model="pwd1" placeholder="请输入新密码"/>
            </div>
            <div class="tel">
                <input type="password" v-model="pwd2" placeholder="确认密码"/>
            </div>
            <div class="yzm" v-if="false">
                <input type="text" placeholder="请输入新密码"/>
                <a>获取验证码</a>
            </div>
        </div>
        <div class="sub_next ">
            <a class="gray" @click="change">保存</a>
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
                thumb:'',
                info:{},
                oldpwd:'',
                pwd1:'',
                pwd2:''
            }
        },
        methods: {
            chose: function (id) {},
            change:function () {
                let that = this;
                if(!this.oldpwd){
                    layer.msg('请检查旧密码');
                    return false;
                }
                if(!this.pwd1){
                    layer.msg('请检查密码');
                    return false;
                }
                if(this.pwd1 != this.pwd2){
                    layer.msg('两次输入密码不一致');
                    return false;
                }
                this.Http('user/changepwd',{
                    oldpwd:that.oldpwd,
                    pwd:that.pwd2
                },function (res) {
                   layer.msg(res.msg)
                })
            },
            exiter:function () {
                let that = this;
                layer.tips(["是","否"],'',function (e) {
                    if(e == '是'){
                        cookie.del('user_id');
                        cookie.del('user_nickname');
                        cookie.del('user_token');
                        layer.msg('退出成功',3,function () {
                            that.href('login')
                        })
                    }
                });
            },
            delCache:function () {
                layer.loading('清理中...');
                new Promise(function () {
                    setTimeout(function () {
                        layer.loading(false);
                        layer.msg('清理完成')
                    },1000)
                })
            }
        },
        created: function () {
            units.title.set('修改密码');
        }
    }
</script>
