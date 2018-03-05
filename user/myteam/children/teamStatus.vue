<!--执行管理-->
<template>
    <div class="find">
        <div class="header" v-if="!search">
            <a @click='goReturn' class="go_return"></a>
            <p class="title">
                <a @click="changeTab(1)" :class="{'currer':current}">团队订单</a>
                <a @click="changeTab(2)" :class="{'currer':current1}">订单总值</a>
            </p>
            <!--<a class="right" @click="startSearch"></a>-->
        </div>
        <headers v-if="search">
            <div class="batten">
                <input class="text" v-model="searchKeyword" type="text" placeholder="请输入车牌关键词进行搜索"/>
                <p @click="startSearch()">取消</p>
            </div>
        </headers>

        <div class="center">
            <ul class="nav" v-show='currentID == 1'>
                <li @click="menuChange(x,index+1)"
                    v-for="(x,index) in menu"
                    :key='index'
                    :class="{'cur':x.curr}">
                    <span v-if="x.name != '待接单' || currentID != 2">{{x.name}}</span>
                    <span v-else>交接中</span>
                </li>
            </ul>
            
             <div class="find_cen" v-show='currentID === 1&&menuFlag'>
                <div class="yzd" v-if='x.card_number' v-for="x in list">
                    <ul class="" @click.stop="gotun(x)">
                        <i class="yzd_img" v-if="x.ex_status == 4"><img src="../../../../assets/img/section.png"></i>
                        <li class="p1"><p>车牌号码</p>
                            <p>发布时间</p>
                            <p>车辆状态</p></li>
                        <li class="must">
                            <p>{{x.card_number}}</p>
                            <p>{{len(x.ex_addtime)}}</p>
                            <p class="teack" style="color:blue">
                                <!-- <span v-if="x.ex_status == 1 || x.ex_status == 2">执行中</span>
                                <span v-if="x.ex_status == 3">交接中</span>
                                <span v-if="x.ex_status == 4">已完成</span> -->

                                <!-- 委托方 -->
                                <!-- <span v-if="(x.ex_status == 1 && currentID==1) ||(x.ex_status == 2 && currentID==1) ">回收中</span>
                                <span v-if="x.ex_status == 0">待接单</span>
                                <span v-if="(x.ex_status == 3 && currentID==1) ||(x.ex_status == 4 && currentID==1) ">已完成</span> -->

                                <!-- 执行方 -->
                                
                                <span v-if="x.ex_status == 2&&currentID==1">回收中</span>
                                <span v-if="(x.ex_status == 3 && currentID==1)">交接中</span>
                                <span v-if="(x.ex_status == 4 && currentID==1) ">已完成</span>
                            </p>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="connection-box">
                
                <div class="shot-number-box shot-number-box-only" v-show='currentID === 2'>
                    <div class="sum-box">
                        <p class="sum-title">订单完成总额度</p>
                        <p class="price"><b>{{orderMoney.total_money}}</b><small>元</small></p>
                    </div>
                    <div class="shot-number">
                        <span class="shot-single">
                            <span class="shot-title">回收中订单数</span>
                            <b>{{orderMoney.order_num_status1}}</b>
                        </span>
                        <span class="shot-single">
                            <span class="shot-title">交接中订单数</span>
                            <b>{{orderMoney.order_num_status2}}</b>
                        </span>
                        <span class="shot-single">
                            <span class="shot-title">已完成订单数</span>
                            <b>{{orderMoney.order_num_status4}}</b>
                        </span>
                    </div>
                </div>
            </div>
            
        </div>
        <!-- <distributionPeople/> -->
    </div>
</template>
<script type="text/javascript">
    import Vue from 'vue';
    import units from '../../../../tools/units'
    import distributionPeople from '@/components/find/distributionPeople'
    import cookie from '../../../../tools/cookie';
    export default {
        name: 'index',
        data () {
            return {
                list: [],
                flag:true,
                leavel:0,
                page:1,
                menuFlag: true,
                menuFlag1: false,
                menu:[
                    {name:'回收中',curr:true},
                    {name:'交接中'},
                    {name:'已完成'}],
                menu1:[
                    {name:'拍摄数量',curr:true},
                    {name:'订单总值'}],
                current:true,
                current1:false,
                currentID:1,
                status:0,
                search:false,
                searchKeyword:'',
                orderMoney: {}, //订单总额
                each_user: ''//每个成员的id
            }
        },
        components: {},
        methods:{
            goReturn () {
                this.$router.go(-1)
            },
            test:function () {
                console.log(1);
            },
            len: function (str) {
                return str.substring(0, 10);
            },
            startSearch:function () {
                this.search = !this.search;
            },
            refresh: function (done) {
                let that = this;
                new Promise(function (a,b) {
                    setTimeout(function () {
                        done();
                    },500)
                })
            },
            infinite: function (done) {
                let that = this;
                setTimeout(function () {
                    if(that.flag) {
                        new Promise(function (a,v) {
                            that.getlist();
                        });
                        done();
                    }else{
                        done(true);
                    }
                }, 1500)
            },
            menuChange:function (item,index) {
                //判断是否为拍摄数量/订单总价
                if(this.currentID == 2){
                    if(index == 0){
                        this.menuFlag =  true
                        this.menuFlag1 =  false
                    }else if(index == 1){
                        this.menuFlag =  false
                        this.menuFlag1 =  true
                        this.getOrderMoneyData()
                    }
                }
                
                this.status = index;
                this.$nextTick(function () {
                    this.menu.forEach(function (item) {
                        Vue.set(item,'curr',false);
                    });
                    this.menu1.forEach(function (item) {
                        Vue.set(item,'curr',false);
                    });
                    Vue.set(item,'curr',true);
                    this.inits(index);
                    // console.log(this.menu);
                    
                    
                });
            },
            getOrderMoneyData(){
                this.$http.post(units.host('statisticsOrderByUser'), {
                    user_id: cookie.get('user_id'),
                    role: cookie.get('role'),
                    order_by: this.order_by 
                }).then(function (res) {
                    // console.log(res)
                    this.orderMoney = res.body.info
                });
            },
            inits:function (index=1) {
                this.page = 1;
                this.flag = true;
                this.list = [];
                this.status = index;
                this.getlist();
            },
            getlist:function () {
                let that = this;
                
                var vip;
                if(!localStorage.getItem('isVIP')){
                     vip = 0;
                } else {
                    vip = 1;
                }
                this.Http('find/findOrderlist',{
                    page:that.page++,
                    status:that.status,
                    currentID:that.currentID+1, //1 执行方,2委托方
                    uid:that.each_user
                },function (res) {

                    if(res.info.current_page >= res.info.last_page){
                        that.flag = false;
                    }
                    for(let x in res.info.data){
                        that.list.push(res.info.data[x])
                    }
                })
            },
            changeTab (ids) {
                this.currentID = ids;
                if(ids == 1) {  
                    this.current = true;
                    this.current1 = false;
                    this.change();
                } else {
                    this.getOrderMoneyData()
                    this.current = false;
                    this.current1 = true;
                }
                
            },
            okayOrder:function (item) {
                let that = this;
                this.Http('find/okay',{
                    orderID:item.ex_oid,
                    status:that.status,
                    card_order:item.card_order,
                    currentID:that.currentID
                },function (res) {
                    layer.msg(res.msg,2,function () {
                        if(res.code > 0){
                            that.inits();
                        }
                    });
                })
            },
            change:function (cur=0) {
                for (let x in  this.menu){
                    this.menu[x].curr = false;
                }
                this.menu[cur].curr = true;
                this.inits(cur+1);
            }
        },
        created: function () {
            let cur = this.$route.query.cur;
            let type = this.$route.query.type;
            if(type) this.current = type;
            if(cur) this.change(cur);
            this.$store.state.header.left = function () {
                location.href = '#/server/start';
            };
            this.each_user = this.$route.query.each_user
            this.change();
        },
        components: {
            distributionPeople
        }
    }
</script>
<!--页面css样式-->
<style scoped lang='scss'>
    .header {
        /*margin-top: 0.3rem;*/
    }
    .center{
        padding-top:1.25rem; 
    }
    .batten {
        height: 1.25rem;
        line-height: 1.25rem;
        background-color: #3d7fed;
        z-index: 999;
        // font-family: 微软雅黑;
        // font-family: 'Droidsansfallback';
        padding: 0 0.5rem;
        padding-top: 0.24rem;
    }

    .text {
        width: 90%;
        height: 0.8rem;
        line-height: 0.8rem;
        color: #fff;
        font-size: 0.3rem;
        float: left;
        border-radius: 1rem;
        text-indent: 0.3rem;
        background: #5697fe url(../../../../assets/img/sous.png) no-repeat center left 0.2rem;
        background-size: 7%;
        padding-left: 0.7rem;
    }

    .batten p {
        float: right;
        font-size: 0.3rem;
        color: #fff;
        margin-top: -0.28rem;
    }
    .header > p {
        text-align: center;
        font-size: 0.44rem;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        color: #fff;
        margin-left: 1rem;
        margin-right: 1rem;
        height: 1.25rem;
    }

    .header > p a {
        color: #fff;
        padding: 0.1rem 0.5rem;
        border-radius: 0.5rem;
        margin-left: 0.6rem;
        margin-right: 0.6rem;
    }

    .header > p a.currer {
        color: #fff;
        padding: 0.1rem 0.5rem;
        background: #5395fd;
        border-radius: 0.1rem;
        margin-left: 0.6rem;
        margin-right: 0.6rem;
    }

    .nav {
        width: 100%;
        height: 1rem;
        background: #fff;
        display: flex;
    }

    .nav li {
        font-size: 0.32rem;
        color: #B4B4B4;
        flex: 1;
        margin-left: 0.71rem;
        margin-right: 0.71rem;
        float: left;
        line-height: 1rem;
        text-align: center;
    }

    .nav li.cur {
        border-bottom: 2px solid #0c80fe;
        color: #1D1D1D;
        width: 20%;
        margin-left: 0.71rem;
        margin-right: 0.71rem;
    }

    .yzd {
        width: 93%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.3rem;
      overflow: hidden;

    }

    .yzd ul {
        background: #fff;
        padding: 0.3rem 0;
        width: 100%;
        background-size: 100% 100%;
    }

    .yzd ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .yzd ul li p {
        display: inline-block;
        float: left;
        width: 33%;
    }

    .yzd ul li.must {
        color: #787878;
    }

    .yzd div {
        width: 15%;
        background: #73a7fc;
        color: #fff;
        font-size: 0.6rem;
        text-align: center;
        height: 2.9rem;
        float: right;
        writing-mode: vertical-lr;
        padding-left: 0.3rem;
    }

    .yzd ul li a.a1 {
        width: 25%;
        margin-top: -0.09rem;
        float: left;
        display: block;
        margin-left: 0.3rem;
    }

    .yzd ul li a.a2 {
        width: 25%;
        margin-top: -0.09rem;
        float: right;
        display: block;
        margin-right: 0.3rem;
    }

    .yzd ul li a img {
        width: 100%;
    }

    .yzd .teack {
        color: #0c80fe;
    }

    .right {
        background: url(../../../../assets/img/img_46.jpg) no-repeat;
        position: absolute;
        top: 0;
        right: 0;
        padding-left: 1.3rem;
        height: 100%;
        background-position: 0.45rem center;
        line-height: 1.2rem;
        background-size: 0.5rem auto;
        vertical-align: middle;
    }
    .yzd_img {
      width: 40%;
      width: 20%;
      display: block;
      position: absolute;
      margin-top: -0.6rem;
      right: 3.3rem;
    }

    .yzd_img img {
      width: 100%;
    }
    .connection-box{
        padding:0 .4rem 0 .4rem;
        font-size: .5rem;
        background: #f0f4fa;
        .shot-number-box{
            margin-top: .6rem;
            background: #fff;
            padding:0 .4rem; 
            border-radius: .2rem;
            .sum-box{
                text-align: center;
                .sum-title{
                   padding-top: .5rem;
                   font-size: .4rem;
                   font-weight: bold;
                }
                .price{
                    color:#2c7dfe;
                    margin-top:.2rem; 
                     b{
                        font-size: .75rem;
                        margin-right: .2rem;
                    }
                }
            }
            h5{
                font-size: .52rem;
                line-height: 1.5rem;
            }
            .shot-number{
                border-top: .01rem solid #eee;
                display: flex;
                justify-content: space-between;
                .shot-single{
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    flex-direction: column;
                    .shot-title{
                        font-size: .35rem;
                        padding-top:.35rem; 
                    }
                    b{
                        color:#2c7dfe;
                        line-height: 1.2rem;
                    }
                }
                
            }
        }
    }
    .shot-number-box-only{
        padding-bottom: 1rem;
    }
</style>