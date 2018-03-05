<template>
    <div>
        <div class="botton">
            <ul>
                <li :class="{cur:current[0]}" @click="goto('','',0)">
                    <img v-if="!current[0]" src="../../assets/img/btn_icon1.png">
                    <img src="../../assets/img/btn_icon2.png" v-else="">
                    <p>无维易寻</p>
                </li>
                <li :class="{cur:current[1]}" @click="goto('server/start',true,1)">
                    <img v-if="!current[1]" src="../../assets/img/btn_icon3.png">
                    <img v-else src="../../assets/img/btn_icon4.png">
                    <p>业务管理</p>
                </li>
                <li :class="{cur:current[2]}" @click="goto('message/list','',2)">
                    <img v-if="!current[2]" src="../../assets/img/btn_icon5.png">
                    <img v-else src="../../assets/img/btn_icon6.png">
                    <p>我的消息</p>
                </li>
                <li :class="{cur:current[3]}" @click="goto('user/index',true,3)">
                    <img v-if="!current[3]" src="../../assets/img/btn_icon7.png">
                    <img v-else src="../../assets/img/btn_icon8.png">
                    <p>个人中心</p>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
    import cookie from '../../tools/cookie'
    import units from '../../tools/units'
    export default {
        props: ['navID'],
        data () {
            return {
                current:[true,false,false,false]
            }
        },
        methods: {
            setcur:function (curr) {
                cookie.set('curr',curr);
                for(let x in this.current){
                    this.current[x] = false;
                }
                this.current[curr] = true;
            },
            goto:function (url,login,curr) {
                if(curr == 1 || curr == 2) {
                    if(cookie.get('user_auth') == 0 ) {
                        layer.msg('请先进行资料认证')
                        return false;
                    }
                }
                this.setcur(curr);
                if(login && !units.isLogin()){
                    this.href('login');
                }else{
                    this.href(url)
                }
            }
        },
        created: function () {
            let curr = cookie.get('curr');
            this.setcur(curr);
        },
        beforeCreate:function () {
            if(this.$route.name == 'index'){
                cookie.set('curr',0);
            }
        },
    }
</script>
<style scoped>
    .botton{
        height: 1.6rem;
        position: fixed;
        bottom: 0;
        left: 0;
        background: #fff;
        width: 100%;
        z-index: 9999;
        -moz-box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.5);
        -webkit-box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.5);
        box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.2);
    }
    .botton ul li{
        display: inline-block;
        width: 25%;
        float: left;
        text-align: center;
        padding-top: 0.2rem;
    }
    .botton ul li p{
        font-size: 0.28rem;
        color: #999;
      margin-top: 0.1rem;
    }
    .botton ul li img{
        width: 0.6rem;
        height: 0.6rem;
        display: block;
        margin: 0 auto;
    }
    .botton ul li.cur p{
      color: #377bee;
    }
    .botton ul li.cur img{
        width: 0.6rem;
        height: 0.6rem;
        display: block;
        margin: 0 auto;
    }
</style>
