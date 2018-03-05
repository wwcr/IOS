<template>
    <div class="details" style="padding-top: 1.25rem;">
        <!-- <ul class="nav">
            <li :class="{'cur':menu1}" @click="menuChange(0)">订单信息</li>
            <li :class="{'cur':menu2}" @click="menuChange(1)">车辆信息</li>
        </ul> -->
        <div class="center" ><!--v-if="menu1"-->
            <div class="list" >
                <p>合同类型：<span>回收</span></p>
                <p>车辆品牌：<span>{{details.ex_brand}}</span></p>
                <p v-if="details.ex_uid == mine_user_id ||details.assign_id == mine_user_id ||details.single_uid == mine_user_id">车牌号码：<span class="orange">{{details.card_number}}</span></p><!--{{details.card_number}}-->
                <p v-else>车牌号码：<span class="orange">******</span></p>
                <!-- <p>车辆佣金：<span style='color:red;'>{{details.ex_money}}元</span></p> -->
                <p class="com"  v-if='details.ex_uid == mine_user_id || isVIP == 1 ||details.assign_id == mine_user_id'>车辆佣金：<span style='color:red;'>{{details.ex_money}}<i>元</i></span></p>
                <p class="com" v-else>车辆佣金：<span><b style="position:relative;top: 0.1rem;color:red;">******</b><i>元</i></span></p>
                <p>G&#12288;P&#12288;S：<span>
                    <span v-if="details.ex_gps == '是'">有</span><!--finds.ex_gps-->
                    <span v-if="details.ex_gps == '否'">无</span>
                </span></p>
                <p v-if='details.gps_platform&&qd'>GPS账号：<span>{{details.gps_platform}}</span></p>
                <p v-if='details.gps_user&&qd'>账&#12288;&#12288;号：<span>{{details.gps_user}}</span></p>
                <p v-if='details.gps_pwd&&qd'>密&#12288;&#12288;码：<span>{{details.gps_pwd}}</span></p>
                <p>回收期限：<span>{{parseInt((details.ex_term-new Date()*1/1000)/3600/24)}}天</span></p>
                <!-- <p>催收诉求：<span class="blue">回抵</span></p> -->
                <!-- <p v-if="hide">订单等级：<span class="orange">{{getType(details.ex_leavel)}}</span></p> -->
            </div>
            <!-- <div class="list">
                <p>债务类型：<span>车贷</span></p>
            </div> -->
        </div>
        <!--<div class="center" v-if="menu2" >
            <div class="list">
                 <p>车辆品牌：<span>{{finds.card_brand}}</span></p>
                <p>车辆型号：<span class="blue">{{finds.card_model}}</span></p>{{finds.card_model}}
                <p v-if="mef">车牌号码：<span class="orange">{{finds.card_number}}</span></p>
                <p v-if="!mef">车牌号码：<span class="orange">******</span></p>
                <p>车辆颜色：<span>{{finds.card_color}}</span></p> 
                <p>G&#12288;P&#12288;S：<span>
                    <span v-if="finds.ex_gps">有</span>
                    <span v-else>无</span>
                </span></p>
                <p>车&#8194;钥&#8194;匙：<span>无</span></p>
                <p>违章记录：<span>
                    <span v-if="finds.ex_virecord">有</span>
                    <span v-else>无</span>
                </span></p>
                <p>疑似位置：<span>{{finds.ex_location}}</span></p>
            </div>
            <div class="list">
                <p>违章内容：<span>无</span></p>
            </div> 
        </div>-->
        <tips v-if="start">
            <div class="fixed-ad-img">
                <img src="../../assets/img/suss.png">
                <div class="point">
                    <a class="look" @click="href('find/index')"><img src="../../../src/assets/img/chakan.png"></a>
                    <a class="goon" @click="href('order/list')"><img src="../../../src/assets/img/jixu.png"></a>
                </div>
                <div class="close-fixed-ad" @click="startfn "></div>
            </div>
        </tips>
        <div class="sub_btn" v-if='finds'>
            <a @click="postData" v-if="!qd">
                <span>抢&emsp;单</span>
            </a>
            <a style="background:#cccccc" v-if="qd" @click="postData">
                <span>已&emsp;抢&emsp;单</span>
            </a>
        </div>
        <!-- 提示订单详情遮罩 -->
        <div class="order-mark-box" v-if='detailFlag'>
            <div class="order-alert">
                <h6>提&nbsp;&nbsp;示</h6>
                <p>您好！您没有抢单权限,如有疑问请联系您所在区域的大区经理。刘经理：010-84685455</p>
                <button style="cursor: pointer;" class="close-alert" @click="sureAlert"></button>
            </div>
        </div>
    </div>
</template>
<script>
    import Vue from 'vue';
    import units from '../../tools/units'
    import navcate from './../template/navcate.vue'
    import tips from '../template/popup.vue'
    import cookie from '../../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                details: {},
                flag: true,
                leavel: 0,
                page: 1,
                menu1:true,
                menu2:false,
                finds:{},
                start:false,
                qd:false,
                hide:false,
                mef:false,
                detailFlag: false,
                m:1,
                mine_user_id: '',
                isVIP: ''
            }
        },
        components: {
            tips
        },
        watch:{
            'menu1':function () {
                // console.log(this.menu2);
                if(this.menu2){
                    this.getlist2();
                }
            }
        },
        methods: {
            menuChange: function (item) {
                this.menu1 = !this.menu1;
                this.menu2 = !this.menu2;
            },
            getType: function (id) {
                if (id == 0) return '特级';
                if (id == 1) return '一级';
                if (id == 2) return '二级';
                if (id == 3) return '三级';
            },
            // getlist2:function () {
            //     let that = this;
            //     if (!that.flag) return false;
            //     that.Http('find/details', {
            //         id: that.$route.query.id
            //     }, function (res) {
            //         console.log(res, that.$route.query.id)
            //         that.finds = res.info;
            //         console.log(res)
            //         // if(that.finds.card_uid == cookie.get('user_id')){
            //         //     that.mef = true;
            //         // }
            //     })
            // },
            postData:function () {
                let that = this;
                if(!cookie.get('role')){
                    // layer.msg('您没有权限抢单');
                    that.detailFlag = true
                    return false;
                }
                if(that.qd){
                    layer.msg('此订单已经被抢了');
                    return false;
                }
                this.Http('order/single',{
                    oid:that.$route.query.id
                },function (res) {
                    if(res.code >0){
                        that.qd = true;
                        that.start = !that.start;
                    }else{
                        layer.msg(res.msg);
                    }
                })
            },
            startfn () {
                this.start = !this.start;
                location.href = '#/order/list';
            },
            getlist: function () {
                let that = this;
                if (!that.flag) return false;
                that.Http('order/orderDetails', {
                    id: that.$route.query.id
                }, function (res) {
                    that.details = res.info;
                    console.log(that.details)
                    if(that.details.single_addtime){
                        that.qd = !that.qd;
                    }
                    // if(that.details.card_uid == cookie.get('user_id')){
                    //     that.mef = true;
                    // }
                })
            },
            sureAlert () {
                this.detailFlag = false;
            },
            getCard:function () {

            }
        },
        created: function () {
            units.title.set('订单详情');

            this.mine_user_id = cookie.get('user_id')
            this.isVIP = cookie.get('role')
            this.getlist();
            if(this.$route.query.c == 1){
                this.mef = true;
            }
            if(this.$route.query.m != 1){
                this.menu1 = true;
                this.menu2 = false;
            }else{
                this.menu1 = false;
                this.menu2 = true;
            }
            let cur = this.$route.query.cur;
            let curAc = this.$route.query.curAc;
             if(!this.finds){
                layer.msg('暂无此信息');
                return false;
            }
            if(cur){
                this.$store.state.header.left = function () {
                    // location.href = '#/find/index?cur='+cur+'&curAc='+curAc;
                    location.href = '#/find/index'
                };
            }
        },
        mounted: function () {
        }
    }
</script>
<style scoped lang='scss'>
    .order-mark-box{
        position: fixed;
        top:0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0,0,0,.5);
        z-index: 9999;
        .order-alert{
            width: 8rem;
            height: 5rem;
            background: #fff;
            border-radius: .15rem;
            position: absolute;
            top:0;
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;
            h6{
                color: #ff3520;
                text-align: center;
                padding-top: .45rem 
            }
            p{
                font-size: .3rem;
                padding: .4rem;
            }
            .close-alert{
                width: 7.2rem;
                height: 1rem;
                border-radius: .14rem;
                border: 0;
                outline: none;
                margin:0 .4rem;
                margin-top: .2rem;
                background: url(../../assets/img/order-btn.png) center;
                background-size: 100%;
            }
        }
    }
    .nav {
        width: 100%;
        height: 1rem;
        background: #fff;
    }

    .nav li {
        font-size: 0.32rem;
        color: #b4b4b4;
        width: 20%;
        margin-left: 1.6rem;
        margin-right: 1.6rem;
        float: left;
        line-height: 1rem;
        text-align: center;
    }

    .nav li.cur {
        border-bottom: 2px solid #0c80fe;
        color: #1d1d1d;
        width: 20%;
        margin-left: 1.6rem;
        margin-right: 1.6rem;
    }

    .center {

    }

    .list {
        padding: 0.2rem 0.4rem;
        margin: 0.4rem;
        background: #fff;
        font-size: 0.4rem;
    }

    .list p {
        line-height: 1rem;
        font-size: 0.4rem;
        color: #787878;
    }

    .list p span {
        color: #1e1e1e;
    }

    .list p span.blue {
        color: #2c7dfe;
    }

    .list p span.orange {
        color: #fd8230;
    }

    .sub_btn {
        padding: 0.63rem 0.4rem;
        background: #f2f6f7;
    }
</style>