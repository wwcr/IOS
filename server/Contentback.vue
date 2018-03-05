<!--页面css样式-->
<style scoped lang='scss'>
    .nav {
        width: 100%;
        height: 1rem;
        background: #fff;
    }

    .right {
        float: right !important;
    }
    .nav{
        display: flex;
        justify-content: space-around;
    }
    .nav li {
        font-size: 0.45rem;
        color: #B4B4B4;
        // width: 15%;
        // margin-left: 0.71rem;
        // margin-right: 0.71rem;
        // float: left;
        line-height: 1rem;
        text-align: center;
    }
    .nav span{
        font-size: 0.45rem;
        // color: red !important;
        padding-top: 0;
    }

    .nav li.cur {
        border-bottom: 2px solid #0c80fe;
        color: #1D1D1D;
        width: 15%;
        // margin-left: 0.71rem;
        // margin-right: 0.71rem;
    }

    .list {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.5rem;

    }

    .list ul {
        background: url(../../../src/assets/img/list_bg.png) no-repeat;
        height: 2.9rem;
        width: 100%;
        background-size: 100% 100%;
    }

    .list ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        width: 100%;
        /*background: #fff;*/
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .list ul li p {
        display: inline-block;
        float: left;
        width: 33%;
    }

    .list ul li.must {
        color: #787878;
    }

    .payment {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.5rem;

    }

    .payment ul {
      background: url(../../../src/assets/img/list_bg.png) no-repeat;
        /*height: 2.9rem;*/
        width: 100%;
        background-size: 100% 100%;
        margin-top: 0.3rem;
    }

    .payment ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        width: 100%;
        /*background: #fff;*/
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .payment ul li p {
        display: inline-block;
        float: left;
        width: 33%;
    }

    .payment ul li.must {
        color: #787878;
    }

    .payment ul li a {
        color: #fff;
    }

    .payment .teack {
        color: #0c80fe;
    }

    .con_list ul li p a {
        color: #e65e5e;
    }

    .ul_list {
        margin-bottom: 0.3rem;
        position: relative;
        margin-top: 0.2rem;
    }

    a {
        color: blue;
    }

    .find {
        float: left;
        margin-left: 0.6rem;
    }

    .find img {
        margin-top: -0.1rem;
        width: 0.35rem;
        margin-right: 0.2rem;
    }

    .list ul li a {
        float: right;
        margin-right: 1rem;
        color: #0c80fe;
    }

    .yzd {
        width: 90%;
        margin: 0 auto;
        position: relative;
        margin-top: 0.5rem;

    }

    .yzd ul {
        background: url(../../../src/assets/img/list_bg.png) no-repeat;
        height: 2.9rem;
        width: 100%;
        background-size: 100% 100%;
        margin-top: 0.3rem;
        position: relative;
        overflow: hidden;
    }

    .yzd ul li {
        height: 1rem;
        line-height: 0.9rem;
        text-align: center;
        width: 100%;
        color: #1e1e1e;
        font-size: 0.4rem;
    }

    .yzd ul li p {
        display: inline-block;
        float: left;
        width: 50%;
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
        background: #5697fe url(../../../src/assets/img/sous.png) no-repeat center left 0.2rem;
        background-size: 7%;
        padding-left: 0.7rem;
    }

    .batten p {
        float: right;
        font-size: 0.3rem;
        color: #fff;
        margin-top: -0.28rem;
    }

    ::-webkit-input-placeholder { /* WebKit browsers */
        color: #fff;
    }

    :-moz-placeholder { /* Mozilla Firefox 4 to 18 */
        color: #fff;
    }

    ::-moz-placeholder { /* Mozilla Firefox 19+ */
        color: #fff;
    }

    :-ms-input-placeholder { /* Internet Explorer 10+ */
        color: #fff;
    }

    .load {
        text-align: center;
        font-size: 0.3rem;
        margin-top: 1rem;
        color: #b4b4b4;
    }

    .yzd_img {
        width: 40%;
        width: 20%;
        display: block;
        position: absolute;
        margin-top: -0.4rem;
        right: 3.3rem;
    }

    .yzd_img img {
        width: 100%;
    }

    .flat {
        background: url(../../assets/img/img_end.png);
        background-size: 100% 100%;
        font-size: 0.3rem;
        color: #fff;
        width: 2.5rem;
        height: 0.7rem;
        display: block;
        line-height: 0.7rem;
        float: left;
    }

    .yzm_list {
        margin-top: 0.09rem;
        padding: 0 0.3rem;
    }

    .mode {
        background: url(../../assets/img/img_end.png);
        background-size: 100% 100%;
        font-size: 0.3rem;
        color: #fff;
        width: 2.5rem;
        height: 0.7rem;
        display: block;
        line-height: 0.7rem;
        float: right;
    }
  .pay_list{
    margin-top: 0.09rem;
    padding: 0 0.3rem;
  }
  .pay_list a{
    background: url(../../assets/img/img_end.png);
    background-size: 100% 100%;
    font-size: 0.3rem;
    color: #fff;
    width: 3.5rem;
    height: 0.8rem;
    display: block;
    line-height: 0.8rem;
    float: right;
    margin-top: 0.15rem;
  }
  .timer img{
    width: 0.5rem;
    height: 0.5rem;
    float:left;
    margin-top:0.2rem;
  }
  .count{
    margin-left: 0.2rem;
    float:left;
  }
  .sj-box{ 
      position: relative;
      top: -1rem;
      right: -.8rem;
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
<!--服务详情-->
<template>
    <div class="wrap">
        <headers v-if="search">
            <div class="batten">
                <input class="text" v-model="searchKeyword" type="text" placeholder="请输入车牌关键词进行搜索"/>
                <p @click="noSearch()">取消</p>
            </div>
        </headers>
        <headers v-if="!search"></headers>
        <div class="load" v-if="false">已全部加在完毕</div>
        <div class="content"  style='padding-top:1.25rem;'>
            <ul class="nav" v-if="serverType==1">
                <li :class="{'cur':current[0]}" @click="currentChange(0)">查找中</li>
                <li :class="{'cur':current[1]}" @click="currentChange(1)">付款中</li>
                <li :class="{'cur':current[2]}" @click="currentChange(2)">已找到</li>
            </ul>
            <ul class="nav" v-if="serverType==2">
                <li :class="{'cur':current[0]}" @click="currentChange(0)">查找中</li>
                <li :class="{'cur':current[1]}" @click="currentChange(1)">付款中</li>
                <li :class="{'cur':current[2]}" @click="currentChange(2)">已找到</li>
                <li>
                    
                    <span class="order" @click="getArticle()">
                        时间
                        <span class="sj-box">
                            <b class="up-sj" :class='{jtActive: jtFlag}'></b>
                            <b class="down-sj" :class='{jtActive: !jtFlag}'></b>
                        </span>
                    </span>
                </li>
            </ul>
            <!--查找中-->
            <scroller
                    :on-refresh="refresh"
                    :on-infinite="infinite"
                    noDataText="全部加载完成"
                    ref="myscroller" style="top:78.11px">
                <div class="list" v-if="current[0]">
                    <ul v-for="(x,k) in list" class="ul_list">
                        <li><p class="p1">车牌号码</p>
                            <p>发布时间</p>
                            <p>车辆状态</p></li>
                        <li>
                            <p class="must">{{x.card_number}}</p>
                            <p class="must">{{len(x.card_addtime)}}</p>
                            <p v-if="x.find_id">
                                <a click="href('server/list?sid='+serverType+'&id='+x.find_id)">寻车</a>
                            </p>
                            <p v-else>
                                <a click="href('/server/list?sid='+serverType+'&id='+x.nurse_id)">寻车</a>
                            </p>
                        </li>
                        <li>
                            <span class="find"><img src="../../../src/assets/img/city.png">
                                所在城市：{{x.card_city}}
                            </span>
                        </li>
                    </ul>
                </div>
                <!--付款中-->
                <div class="payment" v-if="current[1]">
                    <ul class="" v-for="(x,k) in list">
                        <li class="p1"><p>车牌号码</p>
                            <p>发布时间</p>
                            <p>车辆状态</p></li>
                        <li class="must">
                            <p>{{x.card_number}}</p>
                            <p>{{len(x.card_addtime)}}</p>
                            <p class="teack">寻车</p>
                        </li>
                        <li class="pay_list">
                        <span class="timer"><img src="../../../src/assets/img/time.png"></span>
                        <span v-show="show" class="count">{{x.ex_time}}</span>
                          <a @click="href('pay?order='+x.card_order)">去付款</a>
                            <!--<a @click="href('pay?order='+x.card_order)">去付款</a>-->

                        </li>
                    </ul>
                </div>
                <!--已找到-->
                <div class="yzd " v-if="current[2]">
                    <ul class="" v-for="x in list">  <!--@click.stop="gotorun(x)" -->
                        <i class="yzd_img"><img src="../../../src/assets/img/section.png"></i>
                        <!--<div @click="href('server/map?id='+x.find_id)">查看车辆</div>-->
                        <li class="p1"><p>车牌号码</p>
                            <p>发布时间</p>
                            <!--<p>车辆状态</p></li>-->
                        <li class="must">
                            <p>{{x.card_number}}</p>
                            <p>{{len(x.card_addtime)}}</p>
                            <!--<p class="teack">套餐</p>-->
                        </li>
                        <li class="yzm_list">
                            <a class="flat" @click.stop="goSend(x.find_id)">平台执行</a>
                            <a class="mode" @click.stop="href('server/navigation?id='+x.card_number)">查看车辆</a>
                            <div v-if="false">
                                <a :class="{right:x.car_status == 3 || x.car_status == 2}" class="a1 flat"
                                   @click.stop="goSend(x.find_id)">
                                    <img src="../../../src/assets/img/but_2.png"></a>
                                <a class="a2 flat" @click.stop="okayOrder(x.find_id)" v-if="x.car_status != 3">
                                    <img src="../../../src/assets/img/queren.png">
                                </a>
                            </div>
                        </li>
                    </ul>
                </div>
            </scroller>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import headers from '../template/header.vue'
    export default {
        name: 'index',
        data () {
            return {
                serverType: 1,
                list: [],
                articlePage: 1,
                articleLimit: 12,
                moreThat: true,
                host: units.getHost(),
                current: [true, false, false],
                currentNum: 0,
                sid: '',
                search: false,
                status: 1,
                searchKeyword: '',
                show: true,
                count: '',
                timer: null,
                order_by:1,
                jtFlag: false
            }
        },
        components: {
            headers
        },
        watch: {
            'searchKeyword': function () {
                let that = this;
                that.list = [];
                this.Http('find/search', {
                    status: that.status,
                    keyword: that.searchKeyword,
                    type: that.currentNum
                }, function (res) {
                    that.list = res.info.data;
                    console.log(that.list)
                    that.moreThat = false;
                })
            }
        },
        methods: {
            gotorun:function (x) {
                console.log(x);
                location.href = '#/server/details?cid='+x.find_id;
            },
            okayOrder: function (id) {
                this.Http('find/okayFind', {
                    id: id,
                    status: 3
                }, function (res) {
                    layer.msg(res.msg, 3, function () {
                        if (res.code > 0) {
                        }
                    })
                })
            },
            test: function () {
                let that = this;
                that.count = 10;
                // setInterval(function() {
                //     // that.count++;
                //       if ((that.count--) <= 0) {
                //         that.count = 10;
                //         // me.sendMsgDisabled = false;
                //         alert(111);
                //         clearInterval();
                //       }
                //     }, 1000);
                 let sh = setTimeout(function () {
                        if ((that.count--) <= 0) {
                        // that.count = 10;
                        alert(111);
                        // clearInterval();
                      }
                    }, 500)
                clearTimeout(sh);
            },
            goSend: function (id) {
                let that = this;
                this.Http('order/Isterrace', {
                    id: id
                }, function (res) {

                    console.log(res.info)
                    if (res.info[0]) {
                        layer.open({
                            content: '您已经发布过此寻车订单了',
                            btn: ['查看订单', '我知道了'],
                            shadeClose: false,
                            yes: function () {
                                layer.closeAll();
                            },
                            no: function () {
                                that.href('order/details?id=' + res.info.ex_oid);
                            }
                        });
                    } else {
                        that.href('server/terrace?id=' + id+'&carId='+res.info[1])
                    }
                });
            },
            refresh: function (done) {
                new Promise(function (a, b) {
                    setTimeout(function () {
                        done();
                    }, 500)
                })
            }, 
            infinite: function (done) {
                let that = this;
                // console.log(1234567);
                setTimeout(function () {
                    if (that.moreThat) {
                        that.getArticle();
                        done();
                    } else {
                        done(true);
                    }
                }, 1500)
            },
            len: function (str) {
                return str.substring(0, 10);
            },
            currentChange: function (id) {
                this.current = [];
                // console.log(id);
                for (let i = 0; i < 3; i++) {
                    if (i == id) {
                        this.current.push(true);
                    } else {
                        this.current.push(false);
                    }
                }
                this.currentNum = id;
                this.list = [];
                this.articlePage = 1;
                this.moreThat = true;
                // console.log(this.currentNum);
                //if (id == 2) this.status = 2;
                this.status = id+1;
                // console.log(this.status);
                this.getArticle(id);
            },
            timeer: function (time) {
                return units.timemake(time)
            },
            moreThatText: function () {
                return this.moreThat == true ? '查看更多' : '全部加载完成';
            },
            noSearch: function () {
                units.title.set('寻车管理');
                this.search = !this.search
            },
            getPayOrder(){
                console.log(this.currentNum);
            },
            getArticle(id){
                this.jtFlag = !this.jtFlag
                let that = this;
                let $url = 'find/listd';
                if(id == undefined){
                    if(this.order_by == 1){
                        this.order_by = 2;
                        that.articlePage--;
                    }else{
                        this.order_by = 1;
                    }
                }else{
                     this.order_by = 1;
                }
                id = this.currentNum;
                if (id == 1) {
                    $url = 'order/status';
                    that.status = 1;
                }
                // console.log(345678);
                // if (!that.moreThat) return false;
                this.Http($url, {
                    // page: that.articlePage++,
                    limit: that.articleLimit,
                    status: that.status,
                    order_by:that.order_by,
                }, function (res) {
                    that.list = res.info.data;
                    let list = that.list
                    // console.log(list)
                    if (res.info.current_page >= res.info.last_page) {
                        that.moreThat = false;
                    }
                    for (let x in list) {
                        var d = new Date(list[x]['card_addtime']); 
                        var youWant=d.getFullYear() + '-' + (d.getMonth() + 1) + '-' + d.getDate() + ' ' + d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds(); 
                        let temp = new Date().Format(youWant.replace(/-/g,"/"));
                         console.log(temp);
                        // new Date(youWant)*1;

                      //当前时间戳
                      //下单距离1小时还剩时间（分钟）
                      if ( id == 1) {
                          var set_id = setInterval(
                            function(){
                            var f = new Date();
                            var youWant1=f.getFullYear() + '/' + (f.getMonth() + 1) + '/' + f.getDate() + ' ' + f.getHours() + ':' + f.getMinutes() + ':' + f.getSeconds(); 
                            console.log(youWant1)
                        let timestamp = eval(new Date(youWant1))*1;
                        console.log(timestamp)
                        let ex_time_s = (3600 - (timestamp-temp)/1000)%60;
                        let ex_time_m = Math.floor((3600 - (timestamp-temp)/1000)/60);
                        if(ex_time_s < 10 && ex_time_s >= 0){
                            ex_time_s = '0' + ex_time_s;
                        }
                        if(ex_time_m < 10 && ex_time_m >= 0){
                            ex_time_m = '0' + ex_time_m;
                        }
                        // console.log(ex_time_m);
                        // console.log(ex_time_s);
                        let ex_time = ex_time_m + ':' + ex_time_s;
                        console.log(ex_time)
                          if(ex_time_s <= 0 && ex_time_m <= 0){
                            //  that.Http('find/listd_delete', {
                            //     order_no: list[x]['card_order'],
                            // }, function (res) {
                            //     // console.log(res);
                            //     if(res.info == '订单已删除'){
                            //     // location.reload();
                            // }
                            // });
                              clearInterval(set_id);
                              return false;
                          }
                            that.$set(list[x],'ex_time',ex_time)
                           },1000);//一分钟一次
                      }
                        // console.log(that.list)
                        // that.list.push(list[x]);
                    }
                });
            }
        },
         getCode:function(){
            alert(111);
         // const TIME_COUNT = 60;
         // if (!this.timer) {
         //   this.count = TIME_COUNT;
         //   this.show = false;
         //   this.timer = setInterval(() => {
         //   if (this.count > 0 && this.count <= TIME_COUNT) {
         //     this.count--;
         //    } else {
         //     this.show = true;
         //     clearInterval(this.timer);
         //     this.timer = null;
         //    }
         //   }, 1000)
         //  }
         } ,
        beforeCreate: function () {
            this.$store.state.header.open = false;
        },
        created: function () {
            units.title.set('寻车管理');
            this.serverType = 2;
            this.$store.state.header.right = true;
            let that = this;
            this.$store.state.header.rightTouch = function () {
                that.noSearch();
            };
            this.$store.state.header.left = function () {
                location.href = '#/server/start';
            };
            let curs = this.$route.query.cur;
            if(curs){
                this.currentChange(parseInt(curs));
            }else{
                this.getArticle(2);
            }
        },
        mounted: function () {

        }
    }
</script>
