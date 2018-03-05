<!--页面css样式-->
<style scoped>
    .logo{
        width: 100%;
    }
    .logo img{
        width: 100%;
    }
    .pass{
        padding: 1rem 1.3rem;
    }
    .pass_inp{
        height: 1.5rem;
        line-height: 1.3rem;
        border-bottom: 1px solid #f1f1f1;
        margin-bottom: 0.5rem;
    }
    .pass_inp input{
        border:none;
        width: 80%;
        overflow: hidden;
        font-size: 0.4rem;/*
        height: 0.7rem;
        padding: 0.1rem 0;*/
    }
    .pass_inp input.text_a{
        width: 40%!important;
    }
    .huoqu{
        float: right;
        width: 40%;
        height: 1rem;
        line-height: 1rem;
        text-align: center;
        border:1px solid #3d7fed;
        color: #3d7fed;
        border-radius:38px;
        font-size: 0.4rem;
        margin-top: 0.2rem;
    }
    .pass_inp img{
        width: 0.44rem;
        height: 0.52rem;
        margin-right: 0.2rem;
    }
    .dianji a{
        color: #377bee;
        font-size: 0.38rem;
    }
    .dianji .dian_l{
        float: left;
    }
    .dianji .dian_r{
        float: right;
    }
    .sub_next a{
        padding:0 1.3rem;
    }
    .sub_next{
        width: 80%;
        text-align: center;
        margin: 0 auto;
        background: none;
    }
    input.text{
        text-indent: 0.2rem;
    }
  .eye{
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
  .open{
    position: relative;
  }
    .company{
      color: #999;
      font-size: 0.3rem;
      position: absolute;
      bottom: 3%;
      left: 35%;
    }
  .company a{
    color: #0c80fe;
  }
</style>
<template>
    <div id="login">
        <div class="logo">
            <img src="../assets/img/logo.jpg">
        </div>
        <div class="pass">
            <div class="pass_inp">
                <img src="../assets/img/img_4.png">
                <input type="tel" class="text" v-model="form.username" placeholder="手机号/邮箱/用户名">
            </div>
            <div class="pass_inp open">
                <img src="../assets/img/img_26.png">
                <input v-if="pwdpass" type="password" class="text" placeholder="密码" v-model="form.password">
                <input v-else type="text" class="text" placeholder="密码" v-model="form.password">
                <div class='eye' :class="{close:eys_close}" @click="eye_click"></div>
            </div>
            <div class="dianji">
                <a @click="href('register?type=1')" class="dian_l">忘记密码</a>
                <a @click="href('register')" class="dian_r">用户注册</a>
            </div>
        </div>
        <div class="sub_next">
            <a @click="submit">立即登录</a>
        </div>
      <div class="company">
        <!--用户协议<a href="#/find/agreement">《用户协议》</a>-->
      </div>
    </div>
    <!--登陆-->
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    export default {
        data () {
            return {
                form:{
                    username:'',
                    password:'',
                },
                eys_close:true,
                pwdpass:true
            }
        },
        methods: {
            eye_click(){
                this.pwdpass = !this.pwdpass;
                this.eys_close = !this.eys_close;
            },
            submit(){
                let that = this;
                if(!that.form.username){
                    layer.msg('请检查手机号/邮箱/用户名');
                    return false;
                }
                if(!that.form.password){
                    layer.msg('请检查密码');
                    return false;
                }
                this.$http.post(units.host('login'),this.form).then(function (res) {
                    // console.log(11111,res)
                    layer.msg(res.data.info,2,function () {
                        if(res.data.code > 0){ //判断是否登陆成功
                        // console.log(res.data)
                        
                            cookie.set('c_status',res.data.msg.c_status); //添加签名
                            cookie.set('user_id',res.data.msg.user_id);
                            cookie.set('user_nickname',res.data.msg.user_nickname);
                            cookie.set('user_token',res.data.msg.user_token);
                            let goto = cookie.get('goBack');
                            // console.log(res)
                            // if(goto){
                                // location.href = goto;
                            // }else{
                                location.href = '#/';
                            // }
                            //判断是否为大区经理
                            if (res.body.msg.role == '1') {
                                cookie.set('role',res.body.msg.role)
                                // console.log('大堂经理', res)
                                that.$store.state.isVIP = true
                                localStorage.setItem("isVIP", true);
                                
                            } else {    
                                console.log('普通人')
                                that.$store.state.isVIP = false
                                localStorage.removeItem("isVIP")
                            }
                            console.log()
                            let nowTime = new Date()*1
                            // let startTime = new Date(res.body.msg.sign_start_time).getTime()
                            let endTime = new Date(res.body.msg.sign_end_time).getTime()
                            if(nowTime < endTime && res.body.msg.sign_end_time) {
                                cookie.set('sign_uesr', 1)//已签约
                            } else {
                                cookie.set('sign_uesr', 0)
                            }
                        }else{
                            layer.msg(res.data.info+','+res.data.msg);
                        }
                    })
                });
            }
        },
        created: function () {
            units.title.set('登陆');
        }
    }
</script>
