<template>
    <!--执行订单-->
    <div class="order">
        <div class="header">
            <a @click='goturn' class="go_return"></a>
            <p class="title">{{$store.state.title}}</p>
            <a @click="href('order/releasepage')" class="right_btn"
               style="font-size: 0.44rem;color:#ffffff;line-height:1.25rem;top:0">
                发布
            </a>
        </div>
        <div class="list-box">     
            <ul class="nav" v-if="true">
                <li 
                    v-for="(x,index) in menu" 
                    :key='index'
                    @click="menuChange(x,index)" 
                    :class="{'cur':x.curr}">
                        {{x.name}}
                        <span class="sj-box">
                            <b class="up-sj" :class='{jtActive: !x.jtFlag}'></b>
                            <b class="down-sj" :class='{jtActive: x.jtFlag}'></b>
                        </span>
                    </li>
            </ul>
           <v-scroll ref='aaa' :on-refresh="onRefresh" :on-infinite="onInfinite" :dataList="scrollData">
                <div class="center">
                    <div 
                        class="cent"
                        v-for="(x, ind) in order" 
                        :key='ind'
                        @click="href('order/details?id='+x.ex_oid)">
                        <div class="vehicle">
                             <p class="ve_p">{{x.ex_addtime}}</p><!--车辆抵押 -->
                            <!-- <span>
                                <img v-if="x.ex_leavel == 0" src="../../../src/assets/img/teji.png">
                                <img v-if="x.ex_leavel == 1" src="../../../src/assets/img/yiji.png">
                                <img v-if="x.ex_leavel == 2" src="../../../src/assets/img/two.png">
                                <img v-if="x.ex_leavel == 3" src="../../../src/assets/img/sanji.png">
                                <img v-if="x.ex_leavel == null" src="../../../src/assets/img/teji.png">
                            </span> -->
                            <!-- <span>{{x.ex_addtime}}</span> -->
                        </div> 
                        <div class="commission"> <!-- clearfix -->
                            <p class="com" v-if='x.ex_uid == mine_user_id || isVIP == 1'>佣金<span>{{x.ex_money}}<i>元</i></span></p>
                            <p class="com" v-else>佣金<span><b style="position:relative;top: 0.3rem;">******</b><i>元</i></span></p>
                            <p class="com comgps" v-if='x.ex_gps == "是"'>GPS:<span>有<i></i></span></p>
                            <p class="com comgps" v-if='x.ex_gps == "否"'>GPS:<span style="color:red;">无<i></i></span></p>
                        <div v-if="false">
                            <p class="gps" ：class="{red: x.ex_gps = '否'}">GPS:{{x.ex_gps}}</p>
                            <p class="break" v-if="x.ex_virecord">违章记录：有</p>
                            <p class="break">违章记录：无</p>
                        </div>
                        </div>
                        <div class="overdue clearfix">
                            <ul>
                                <li>
                                    <img src="../../../src/assets/img/address-icon.png">
                                    <p class="li_title">所在位置:<span><i>
                                        {{x.ex_location}}
                                    </i></span></p>
                                </li>
                                <li>
                                    <img src="../../../src/assets/img/time-icon.png">
                                    <p class="li_title">回收期限:<span><i>{{parseInt((x.ex_term-new Date()*1/1000)/3600/24)}}</i>天</span></p>
                                </li>
                                <!-- <li>
                                    <img src="../../../src/assets/img/ove_img3.png">
                                    <p class="li_title">执行天数<span><i>{{x.ex_term_day}}</i></span></p>
                                </li> -->
                            </ul>
                        </div>
                    </div>
                </div>
            </v-scroll>
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
                order: [],
                // jtFlag: true,
                flag:true,
                leavel:0,
                now:'',
                page:1,
                menu:[{name:'发布金额',curr:true, jtFlag: false},{name:'发布时间', jtFlag: false},{name:'GPS', jtFlag: false}],
                order_by:1,
                mine_user_id: '',
                isVIP: '',
                articlePage: 0,
                articleLimit: 9,
                allarticle:'',
                counter: 1, //当前页
                num: 9, // 一页显示多少条
                pageStart: 0, // 开始页数
                pageEnd: 0, // 结束页数
                listdata: [], // 下拉更新数据存放数组
                scrollData: {
                    noFlag: false //暂无更多数据显示
                }
            }
        },
        components: {
            'v-scroll': require("../pull-refresh")
        },
        methods: {
            goturn () {
                location.href='#/'
            },
            menuChange:function (item,index) {
                item.jtFlag = !item.jtFlag
               
                this.$nextTick(function () {
                    this.menu.forEach(function (item) {
                        Vue.set(item,'curr',false);
                    });
                    Vue.set(item,'curr',true);
                    this.page = 1;
                    this.flag = true;
                     console.log(index);
                    console.log(this.leavel);
                    if(index == this.leavel ){
                         this.order.reverse();
                         // console.log(122354376);
                     }else{
                     this.leavel = index;
                        this.getlist();
                    }
                        // 
                     // }
                    // 
                   
                });
            },
            getType:function (id) {
                if(id ==0) return '特级';
                if(id ==1) return '一级';
                if(id ==2) return '二级';
                if(id ==3) return '三级';
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

                // console.log(1111);
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
            onRefresh(done) {
                this.getlist(2);
                // this.getArticle(this.currentNum,1);
                done(); // call done

            },
             onInfinite(done) {
                // console.log(1323);
                this.getlist(3);
                this.counter++;
                let end = this.pageEnd = this.num * this.counter;
                let i = this.pageStart = this.pageEnd - this.num;
                // console.log()
                let more = this.$el.querySelector('.load-more');
                // console.log(more);
                for(i; i < end; i++) {
                    if(i >= 30) {
                        // console.log(more);
                        more.style.display = 'none'; //隐藏加载条
                        //走完数据调用方法
                        this.scrollData.noFlag = true;
                        // console.log(111321231);
                        break;
                    } else {
                        this.listdata.push({
                            date: "2017-06-1"+i,
                            portfolio: "1.5195"+i,
                            drop: i+"+.00 %" ,
                            state: 2
                        })
                        more.style.display = 'none'; //隐藏加载条
                         // console.log(111);
                    }
                }
                done();
            },
            getlist:function (type) {
                let that = this;
                that.scrollData.noFlag = false;
                if(!that.flag) return false;
                if(this.order_by == 1){
                    this.order_by = 2;
                }else{
                    this.order_by = 1;
                }
                if(type == undefined){//上方切换兰
                    that.articlePage = 0;
                    that.articleLimit = 9;
                }
                 if(type == 2){//下拉刷新
                    that.articlePage = 0;
                    this.allLoaded = false;
                }else if(type == 3){//上拉加载
                     that.articlePage = that.articlePage + that.articleLimit;
                    if(that.articlePage + that.articleLimit > that.allarticle){
                        // more.style.display = 'none'; //隐藏加载条
                        //走完数据调用方法
                        that.scrollData.noFlag = true;
                    }
                }
                // console.log(that.scrollData.noFlag);
                that.Http('order/listd_page',{
                    money: that.$route.query.money,
                    limit:that.articleLimit+that.articlePage,
                    release_time: that.$route.query.release_time,
                    recover_time: that.$route.query.recover_time,
                    page:that.page++,
                    leavel:that.leavel,
                    debug:1,
                    order_by:this.order_by
                },function (res) {
                    // console.log(res)
                    if(res.info.current_page >= res.info.last_page){
                        that.flag = false;
                    }
                    that.order = res.info;
                    that.allarticle = res.msg;
                    // console.log(that.order);
                })
            }
        },
        created () {
            units.title.set('回收业务');
            this.mine_user_id = cookie.get('user_id')
            this.isVIP = cookie.get('role')
            this.getlist();
            // this.$store.state.header.left = function () {
            //     alert(11111111111)
            //     location.href = '#/';
            // };
           
        },
        mounted: function () {}
    }
</script>

<style scoped lang='scss'>
  
    .list-box{
        position: fixed;
        top:0;
        bottom: 0;
        left: 0;
        right: 0;
        padding-top:1.25rem; 
    }
    .nav {
        width: 100%;
        height: 1rem;
        display: flex;
        background: #fff;
        justify-content: space-around;
    } 
    .nav li {
        font-size: 0.32rem;
        color: #b4b4b4;
        line-height: 1rem;
        text-align: center;
        display: flex;
        padding-left:.15rem;
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
    }
    .nav li .sj-box .jtActive{
        border-color: #2c7dfe;
        border-left-color: transparent;
        border-right-color: transparent;
    }
    .nav li.cur {
        border-bottom: 2px solid #0c80fe;
        color: #1d1d1d;
    }

    .cent {
        margin: 0.3rem;
        background: #fff;
        border-top: 1px solid #fe452c;
        padding: 0.16rem 0 0 0.19rem;
    }

    .ve_p {
        font-size: 0.3rem;
        color: #1e1e1e;
        // font-weight: 600;
        display: inline-block;
        color: #787878;
    }

    .com {
        font-size: 0.38rem;
        color: #000;
        font-weight: 600;
        display: inline-block;
    }
    .com span {
        font-size: 0.8rem;
        font-weight: 600;
        color: #fe452c;
        margin-left: .2rem;
        
    }

    .comgps{
        padding-bottom: .19rem; 
        span{
            font-size:  .42rem;
            font-weight: normal;
            color: #0ecdb9;
        }
    }
    .com span i {
        font-size: 0.3rem;
        font-style: normal;
        margin-left: 0.1rem;
    }

    .vehicle {
        height: 0.6rem;
        line-height: 0.6rem;
    }

    .vehicle span {
        font-size: .3rem;
        float: right;
        color:#b4b4b4;
    }

    .commission {
        margin-top: 0.45rem;
        margin-bottom: 0.4rem;
        padding: 0 .2rem; 
        display: flex;
        align-items: flex-end;
        justify-content: space-between;
    }

    .gps {
        background: url(../../../src/assets/img/img_wu.png) no-repeat;
        background-size: 100% 100%;
        display: inline-block;
        font-size: 0.35rem;
        color: #2c7dfe;
        height: 0.7rem;
        width: 2.2rem;
        text-indent: 0.9rem;
        line-height: 0.7rem;
        margin-left: 11%;
    }

    .break {
        background: url(../../../src/assets/img/img_icon.png) no-repeat;
        background-size: 100% 100%;
        display: inline-block;
        font-size: 0.35rem;
        color: #2c7dfe;
        height: 0.7rem;
        width: 3.5rem;
        text-indent: 0.9rem;
        line-height: 0.7rem;
    }

    .overdue {
        background: #fff;
        padding: .4rem 0;
        border-top: 1px dashed #f1f1f1;
        ul{
            display: flex;
            li{
                display: flex;
                padding-left: .5rem;
                flex:1;
                p{
                    display: flex;
                    text-align: center;
                }
            }
        }
    }

    .overdue ul li img {
        height: .45rem;
        position: relative;
        top:.02rem;
        right:.3rem;
    }

    .overdue ul li p span i {
        font-style: normal;
    }
    .li_title{
        font-size: 0.25rem;
        color: #b4b4b4;
    }
    .red{
        color: red;
    }
</style>