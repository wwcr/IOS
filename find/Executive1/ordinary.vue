<!--页面css样式-->
<style scoped lang='scss'>
    .header {
        /*margin-top: 0.3rem;*/
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
        background: #5697fe url(../../../assets/img/sous.png) no-repeat center left 0.2rem;
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
        background: url(../../../assets/img/img_46.jpg) no-repeat;
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
      right: 2.3rem;
    }

    .yzd_img img {
      width: 100%;
    }
    .sj-box{ 
        .down-sj{
            font-size: 0;  
            line-height: 0;  
            border-width: .1rem;  
            border-color: #b4b4b4;  
            border-bottom-width: 0;  
            border-style: dashed;  
            border-top-style: solid;  
            border-left-color: transparent;  
            border-right-color: transparent;  
            position: relative;
            top: 0rem;
            left: -.1rem;
        }
        .up-sj{
            font-size: 0;  
            line-height: 0;  
            border-width: .1rem;  
            border-color: #b4b4b4;  
            border-top-width: 0;  
            border-style: dashed;  
            border-bottom-style: solid;  
            border-left-color: transparent;  
            border-right-color: transparent;  
            position: relative;
            top: -.28rem;
            left: .1rem;
        }
    }
    .nav li .sj-box .jtActive{
        border-color: #2c7dfe;
        border-left-color: transparent;
        border-right-color: transparent;
    }
</style>
<!--执行管理-->
<template>
    <div class="find">
        <div class="header" v-if="!search">
            <a @click="$store.state.header.left" class="go_return"></a>
            <p class="title">
                <a @click="changeTab(1)" :class="{'currer':current}">委托方</a>
                <a @click="changeTab1(2)" :class="{'currer':!current}">回收方</a>
            </p>
            <!--<a class="right" @click="startSearch"></a>-->
        </div>
        <headers v-if="search">
            <div class="batten">
                <input class="text" v-model="searchKeyword" type="text" placeholder="请输入车牌关键词进行搜索"/>
                <p @click="startSearch()">取消</p>
            </div>
        </headers>

        <div class="center" style="padding-top:1.25rem;">
            <ul class="nav">
                <li @click="menuChange(x,index+1)"
                    v-for="(x,index) in menu"
                    :class="{'cur':x.curr}">
                    <span v-if="x.name != '待接单' || currentID != 2">
                        {{x.name}}
                    </span>
                    <span v-else>交接中</span>
                </li>
                <li @click="getlist(1)">
                    <span >
                        时间
                        <span class="sj-box">
                            <b class="up-sj" :class='{jtActive: jtFlag}'></b>
                            <b class="down-sj" :class='{jtActive: !jtFlag}'></b>
                        </span>
                    </span>
                </li>
            </ul>
            <scroller
                    :on-refresh="refresh"
                    :on-infinite="infinite"
                    ref="myscroller"
                    noDataText="全部加载完成"
                    style="margin-top:2.25rem">
            <div class="find_cen">
                <div class="yzd" v-if='x.card_number' v-for="x in list">
                    <ul class="" @click.stop="gotun(x)">
                        <!-- <i class="yzd_img" v-if="x.ex_status == 4"><img src="../../../assets/img/section.png"></i> -->
                        <i class="yzd_img" v-if="(x.ex_status == 3 && currentID==1 || x.ex_status == 4 && currentID==1) ||(x.ex_status == 4 && currentID==2)"><img src="../../../assets/img/section.png"></i>
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
                                <span v-if="(x.ex_status == 1 && currentID==1) ||(x.ex_status == 2 && currentID==1) ">回收中</span>
                                <span v-if="x.ex_status == 0">待接单</span>
                                <span v-if="(x.ex_status == 3 && currentID==1) ||(x.ex_status == 4 && currentID==1) ">已完成</span>

                                <!-- 执行方 -->
                                <span v-if="(x.ex_status == 3 && currentID==2)">交接中</span>
                                <span v-if="x.ex_status == 2&&currentID==2">回收中</span>
                                <span v-if="(x.ex_status == 4 && currentID==2) ">已完成</span>
                            </p>
                        </li>
                        <li v-if="(x.ex_status == 2 && currentID==2) || (x.ex_status==3 && currentID==1)">
                        <p  @click.stop="okayOrder(x)" style="float: right">
                            <img v-if="currentID!=2" src="../../../assets/img/queren.png" style="width: 60%;">
                            <img v-else src="../../../assets/img/gobanckj.png" style="width: 60%;">
                        </p>
                      </li>
                    </ul>
                </div>
            </div>
            </scroller>
        </div>
    </div>
</template>
<script type="text/javascript">
    import Vue from 'vue';
    import units from '../../../tools/units'
    import cookie from '@/tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                list: [],
                flag:true,
                leavel:0,
                page:1,
                jtFlag: true,
                menu:[
                    {name:'回收中',curr:true},
                    {name:'待接单'},
                    {name:'已完成'}],
                current:1,
                currentID:1,
                index: 1,
                status:0,
                search:false,
                searchKeyword:'',
                order_by:1,
            }
        },
        components: {},
        methods:{
            test:function () {
                console.log(1);
            },
            gotun:function (x) {
                location.href = '#/order/details?id='+x.ex_oid + '&c=1&cur='+this.currentID+'&type='+this.current;
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
                console.log(localStorage.getItem('isVIP'))
                this.status = index;
                this.index = index
                this.$nextTick(function () {
                    this.menu.forEach(function (item) {
                        Vue.set(item,'curr',false);
                    });
                    Vue.set(item,'curr',true);
                    this.inits(index);
                    // console.log(item, index);
                    // this.$http.post(units.host('userOrderList'), {
                    //     user_id: cookie.get('user_id'),
                    //     status: index
                    // }).then(function (res) {
                    //     this.list = res.body.info
                    //     this.flag = false
                    //     console.log(res.body.info)
                    // });
                });
            },
            inits:function (index=1) {
                console.log(index)
                this.page = 1;
                this.flag = true;
                this.list = [];
                this.status = index;
                this.getlist();
                this.order_by = 1;
            },
            getlist (type) {
                let that = this;
                that.list = []
                if(type == 1){
                    console.log('时间');
                    if(this.order_by == 1){
                        this.jtFlag = !this.jtFlag
                        this.order_by++;
                        that.page--
                    }else{
                        this.jtFlag = !this.jtFlag
                        this.order_by--;
                        that.page--
                    }
                }
                var vip;
                if(!localStorage.getItem('isVIP')){
                     vip = 0;
                } else {
                    vip = 1;
                }
                console.log(vip)
                // this.$http.post(units.host('userOrderList'), {
                //     user_id: cookie.get('user_id'),
                //     status: this.index,
                //     order_by: this.order_by 
                // }).then(function (res) {
                //     this.list = res.body.info
                //     this.flag = false
                //     console.log(res.body.info)
                // });
                this.Http('find/findOrderlist',{
                    page:that.page++,
                    status:that.status,
                    currentID:that.currentID, //1 执行方,2委托方
                    order_by:that.order_by,
                    vip: vip
                },function (res) {

                    if(res.info.current_page >= res.info.last_page){
                        that.flag = false;
                    }
                    for(let x in res.info.data){
                        that.list.push(res.info.data[x])
                    }
                })
            },
            changeTab:function (ids) {
                this.currentID = ids;
                this.current = 1
                this.change();
            },
            changeTab1:function (ids) {
                this.currentID = ids;
                this.current = 0
                this.change();
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
                this.inits(cur);
            }
        },
        created: function () {
            var that = this
            let cur = this.$route.query.cur;
            let type = this.$route.query.type;
            if(type) this.current = type;
            if(cur) this.change(cur);
            this.$store.state.header.left = function () {
                location.href = '#/server/start';
            };

            // this.$http.post(units.host('userOrderList'), {
            //     user_id: cookie.get('user_id'),
            //     status: 1
            // }).then(function (res) {
            //     // that.list = res.body.info
            //     console.log(res)
            // });
        }
    }
</script>
