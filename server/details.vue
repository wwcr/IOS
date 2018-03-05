<style scoped>
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
<template>
    <div class="details" style="padding-top: 1.25rem;">
        <ul class="nav">
            <li :class="{'cur':menu1}" @click="menuChange(0)">订单信息</li>
            <li :class="{'cur':menu2}" @click="menuChange(1)">车辆信息</li>
        </ul>
        <div class="center" v-if="menu1">
            <div class="list" >
                <p>债务类型：<span>车贷</span></p>
                <p>催收诉求：<span class="blue">回抵</span></p>
                <p v-if="hide">订单等级：<span class="orange">{{getType(details.ex_leavel)}}</span></p>
                <p>车辆佣金：<span style='color:red;'>{{details.ex_money}}元</span></p>
                <p>执行截止：<span>{{details.ex_term_day}}天</span></p>
                <p v-if="hide">贷款金额：<span>5000000.00元</span></p>
                <p v-if="hide">逾期金额：<span>0.0</span></p>
                <p v-if="hide">违约金额：<span>0.0</span></p>
                <p v-if="hide">贷款期限：<span>30期</span></p>
            </div>
            <!-- <div class="list">
                <p>债务类型：<span>车贷</span></p>
            </div> -->
        </div>
        <div class="center" v-if="menu2" >
            <div class="list">
                 <p>车辆品牌：<span>{{finds.card_brand}}</span></p><!--{{finds.card_brand}} -->
                <!--<p>车辆型号：<span class="blue">{{finds.card_model}}</span></p>{{finds.card_model}}-->
                <p v-if="mef">车牌号码：<span class="orange">{{finds.card_number}}</span></p><!--{{finds.card_number}}-->
                <p v-if="!mef">车牌号码：<span class="orange">******</span></p>
                <!-- <p>车辆颜色：<span>{{finds.card_color}}</span></p> -->
                <p>G&#12288;P&#12288;S：<span>
                    <span v-if="finds.ex_gps">有</span><!--finds.ex_gps-->
                    <span v-else>无</span>
                </span></p>
                <p>违约城市：<span>北京</span></p><!--{{finds.ex_location}}-->
                <!-- <p>车&#8194;钥&#8194;匙：<span>无</span></p>
                <p>违章记录：<span>
                    <span v-if="finds.ex_virecord">有</span>
                    <span v-else>无</span>
                </span></p>
                <p>疑似位置：<span>{{finds.ex_location}}</span></p> -->
            </div>
            <!-- <div class="list">
                <p>违章内容：<span>无</span></p>
            </div> -->
        </div>
        <tips v-if="start">
            <div class="fixed-ad-img">
                <img src="../../assets/img/suss.png">
                <div class="point">
                    <a class="look" @click="href('find/index')"><img src="../../../src/assets/img/chakan.png"></a>
                    <a class="goon" @click="href('order/list')"><img src="../../../src/assets/img/jixu.png"></a>
                </div>
                <div class="close-fixed-ad" @click="start = !start"></div>
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
                m:1
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
                // if(!this.finds){
                //     layer.msg('暂无此信息');
                // }
                this.menu1 = !this.menu1;
                this.menu2 = !this.menu2;
            },
            getType: function (id) {
                if (id == 0) return '特级';
                if (id == 1) return '一级';
                if (id == 2) return '二级';
                if (id == 3) return '三级';
            },
            getlist2:function () {
                let that = this;
                if (!that.flag) return false;
                that.Http('find/details', {
                    id: that.$route.query.id
                }, function (res) {
                    console.log(res)
                    that.finds = res.info;
                    // if(that.finds.card_uid == cookie.get('user_id')){
                    //     that.mef = true;
                    // }
                })
            },
            postData:function () {
                let that = this;
                if(!cookie.get('role')){
                    layer.msg('您没有权限抢单');
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
            getlist: function () {
                let that = this;
                if (!that.flag) return false;
                that.Http('order/orderDetails', {
                    id: that.$route.query.id
                }, function (res) {
                    that.details = res.info;
                    if(that.details.single_addtime){
                        that.qd = !that.qd;
                    }
                })
            },
            getCard:function () {

            }
        },
        created: function () {
            units.title.set('执行订单');
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
            if(cur){
                this.$store.state.header.left = function () {
                    location.href = '#/find/index?cur='+cur;
                };
            }
        },
        mounted: function () {
        }
    }
</script>
