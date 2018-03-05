<!--页面css样式-->
<style scoped>
    .logo {
        width: 100%;
        padding-top:1.25rem; 
    }

    .logo img {
        width: 100%;
    }

    .pass {
        padding: 0.1rem 1.3rem;
    }

    .pass_inp {
        height: 1.5rem;
        line-height: 1.3rem;
        border-bottom: 1px solid #f1f1f1;
        margin-bottom: 0.5rem;
    }

    .pass_inp input {
        border: none;
        width: 90%;
        overflow: hidden;
        font-size: 0.4rem;
        text-indent: 0.2rem;
        /*
                height: 0.7rem;
                padding: 0.6rem 0;*/
    }

    .pass_inp input.text_a {
        width: 40% !important;
    }

    .huoqu {
        float: right;
        /*width: 40%;*/
        height: 1rem;
        line-height: 1rem;
        text-align: center;
        /*border:1px solid #3d7fed;*/
        color: #3d7fed;
        border-radius: 38px;
        font-size: 0.4rem;
        margin-top: 0.2rem;
    }

    .company {
        color: #999;
        font-size: 0.32rem;
        position: absolute;
        bottom: 3%;
        left: 23%;
    }

    .company a {
        color: #0c80fe;
    }

    .eye {
        background: url(../../src/assets/img/open.png) no-repeat;
        background-size: 100% 100%;
        position: absolute;
        right: 0;
        top: 40%;
        width: 0.6rem;
        height: 0.32rem;
    }
    .close{
        background: url(../../src/assets/img/close.png) no-repeat;
        background-size: 100% 100%;
        position: absolute;
        right: 0;
        top: 40%;
        width: 0.6rem;
        height: 0.32rem;
    }
    .po_reg {
        position: relative;
    }

    .dianji a {
        color: #377bee;
        font-size: 0.38rem;
    }

    .dianji .dian_l {
        float: left;
    }

    .dianji .dian_r {
        float: right;
    }

    .submint {
        background: #a3a3a3;
    }

</style>
<template>
    <div id="Register">
        <div class="logo">
            <img src="../assets/img/logo.jpg">
        </div>
        <div class="pass" v-if="form.type==1">
            <div class="pass_inp">
                <input type="tel" v-model="form.user_mobile" class="text" placeholder="请输入手机号">
            </div>
            <div class="pass_inp">
                <input type="tel" v-model="form.qcode" class="text_a" placeholder="获取短信验证码">
                <a class="huoqu" @click="sendQcode">{{changeText}}</a>
            </div>
            <div class="pass_inp">
                <input type="password" v-model="form.user_password" class="text" placeholder="请输入6-14位英文字母/数字/符号">
            </div>
            <div class="sub_next">
                <a class="" @click="next">找回密码</a>
            </div>
        </div>
        <div class="pass" v-else>
            <!--<div class="pass_inp">-->
            <!--<input type="text" v-model="form.user_username" class="text" placeholder="请填写昵称">-->
            <!--</div>-->

            <div class="pass_inp">
                <input type="tel" v-model="form.user_mobile" class="text" placeholder="请输入手机号">
            </div>
            <div class="pass_inp">
                <input type="tel" v-model="form.qcode" class="text_a" placeholder="获取短信验证码">
                <a class="huoqu" @click="sendQcode">{{changeText}}</a>
            </div>
            <div class="pass_inp po_reg">
                <input v-if="eys_close" type="text" v-model="form.user_password" class="text"
                       placeholder="请输入6-14位英文字母/数字/符号">
                <input v-if="!eys_close" type="password" v-model="form.user_password" class="text"
                       placeholder="请输入6-14位英文字母/数字/符号">
                <div class='eye' :class="{close:!eys_close}" @click="eye_click"></div>
            </div>
            <div class="dianji">
                <a href="#/" class="dian_l">返回首页</a>
                <a href="#/login" class="dian_r">已有账户登陆</a>
            </div>
            <div class="sub_next">
                <a @click="next">注册</a>
            </div>
            <div class="company">
                注册代表您同意用户协议<a href="#/find/agreement">《用户协议》</a>
            </div>
        </div>
    </div>
    <!--注册,忘记秒密码-->
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                form: {
                    user_username: '用户',
                    user_mobile: '',
                    qcode: '',
                    user_password: '',
                    type: ''
                },
                changeText: '获取验证码',
                changeNumber: 90,
                eys_close: false
            }
        },
        methods: {
            eye_click: function () {
                this.eys_close = !this.eys_close
            },
            sendQcode: function () {
                let that = this;
                if (this.form.user_mobile) {
                    this.$http.post(units.domin('Sms/forget'), units.params(this.form)).then(function (res) {
                        if (res.data.code > 0) {
                            layer.msg(res.data.info, 2, function () {
                                that.changetime();
                            });
                        } else {
                            layer.msg(res.data.msg)
                        }
                    });
                } else {
                    layer.msg('请检查手机号')
                }
            },
            changetime: function () {
                let that = this;
                let timeer = setInterval(function () {
                    that.changeNumber--;
                    if (that.changeNumber <= 0) {
                        that.changeText = '重新获取验证码';
                        clearInterval(timeer);
                    } else {
                        that.changeText = that.changeNumber + '秒后重新获取';
                    }
                }, 1000)
            },
            validate: function (fn) {
                let that = this;
                let tips = ['昵称', '手机号', '验证码', '密码'];
                let from = this.form;
                let num = -1;
                let next = false;
                $.each(from, function (k, value) {
                    num++;
                    if (!value && k != 'type') {
                        layer.msg('请检查' + tips[num]);
                        next = true;
                        return false;
                    }
                });
                fn && fn(next)
            },
            postData(){
                let that = this;
                this.validate(function (res) {
                    if (!res) {
                        that.$http.post(units.host('Register'), units.params(that.form)).then(function (res) {
                            if (res.data.code > 0) {
                                cookie.set('user_id', res.data.msg.user_id);
                                cookie.set('user_nickname', res.data.msg.user_nickname);
                                cookie.set('user_token', res.data.msg.user_token)
                                //判断是否为大堂经理
                                if (res.body.msg.role == '1') {
                                    console.log('大堂经理', res)
                                    that.$store.state.isVIP = true
                                    localStorage.setItem("isVIP", true);
                                    
                                } else {    
                                    console.log('普通人')
                                    that.$store.state.isVIP = false
                                    localStorage.removeItem("isVIP")
                                }
                                layer.msg(res.data.info, 2, function () {
                                    location.href = '#/metype';
                                })
                            } else {
                                layer.msg(res.data.info + ',' + res.data.msg);
                            }
                        });
                    }
                })
            },
            forget: function () {
                let that = this;
                if(!that.form.user_mobile){
                    layer.msg('请检查手机号');
                    return false;
                }
                if(!that.form.qcode){
                    layer.msg('请检查验证码');
                    return false;
                }
                if(!that.form.user_password){
                    layer.msg('请检查密码');
                    return false;
                }
                that.$http.post(units.host('forget'), units.params(that.form)).then(function (res) {
                    if (res.data.code > 0) {
                        layer.msg(res.data.info, 2, function () {
                            location.href = '#/login';
                        })
                    } else {
                        console.log(res.data);
                        layer.msg(res.data.info + ',' + res.data.msg);
                    }
                });
            },
            next: function () {
                if (this.form.type == 1) {
                    this.forget();
                } else {
                    this.postData();
                }
            }
        },
        created: function () {
            this.form.type = this.$route.query.type;
            if (this.form.type) {
                units.title.set('忘记密码')
            } else {
                units.title.set('注册账号')
            }
        }
    }
</script>
