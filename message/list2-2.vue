<!--页面css样式-->
<style scoped lang='scss'>
    .message {
        background: #f0f4fa;
    }

    .message ul {
        background: #fff;
        margin-bottom: 0.3rem;
    }

    .message ul li {
        margin-left: 0.15rem;
        border-bottom: 1px solid #cccccc;
        padding: 0.1rem 0 0.3rem 0.3rem;
        height:60px;
    }

    .message ul li .img {
        float: left;
        margin-right: 0.3rem;
        position: relative;
    }

    .message ul li .img img {
        width: 1.7rem;
        height: 1.7rem;
        margin-bottom:5px;
    }

    .message ul li .mess {
        display: inline-block;
        margin-top: 0.1rem;
    }

    .message ul li h5 {
        font-size: 0.32rem;
    }

    .message ul li .p1 {
        font-size: 0.35rem;
        color: #787878;
        margin-top: 0.1rem;
    }

    .message ul li .p2 {
        font-size: 0.35rem;
        color: #787878;
        margin-top: 0.2rem;
    }
    .img i{
      width: 0.3rem;
      height: 0.3rem;
      background: red;
      position: absolute;
      right: 0.5rem;
      top: 0;
      border-radius: 50%;
    }
    .mess h5{
        font-size: 0.4rem!important;
        font-weight: 400;
    }
    /*#ul .mint-cell-value{
        display: none !important;

    }*/
    .message ul li .img{
        margin-left: -10rem !important;
    }
    .message ul li .mess{
        margin-left: 0.3rem !important;
    }
    .mint-cell-swipe-button{
        font-size: 10px !important;
    }
    .mint-cell:last-child{
        background-image: linear-gradient(180deg,#fff,#fff 50%,transparent 0)!important;
    }
    .mess{
        width: 7rem!important;
        .p1{
             overflow:hidden;
            text-overflow:ellipsis;
            white-space:nowrap
        }
    }
    
</style>
<!--服务列表-->
<template>
    <div class="message">
        <scroller
                :on-refresh="refresh"
                :on-infinite="infinite"
                ref="myscroller"
                noDataText="全部加载完成"
                style="margin-top:1.5rem">
            <ul v-if="info.length > 0" id="ul">
                <li v-for="(x,k) in info" @click="getContent(x.rid, x.mid, x, k)">
                    <mt-cell-swipe
                      :right="[
                        {
                          content: '删除',
                          style: { background: '#ff4040', color: '#fff', fontSize:'16px', width:'2rem', textAlign:'center'},
                          handler: () => messagebox(x.rid, k)
                        }
                      ]">
                        <div class="img" style="margin-left:-3rem;">
                            <img :src="getIcon()" style="width:40px;height:40px">
                            <i v-if="x.is_readed == 0" ></i>
                        </div>
                        <div class="mess">
                            <h5>{{x.title}}</h5>
                            <p class="p1">{{x.content}}</p>
                            <!-- <p class="p1">{{x.content.slice(0,25)+ '...'}}</p> -->
                            <p class="p2">{{formatDateTime(x.date*1000)}}</p>
                        </div>
                    </mt-cell-swipe>
                </li>
            </ul>
        </scroller>
        <navcate></navcate>
    </div>
</template>
<script>
    import Vue from 'vue'
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    import { CellSwipe } from 'mint-ui';
    // Vue.component(CellSwipe.name, CellSwipe);

    export default {
        name: 'index',
        data () {
            return {
                content : 'asdas',
                info: {},
                ready:{},
                icon:['img_img1.png','img_img2.png','img_img3.png','img_img4.png']
            }
        },
        components: {
            navcate
        },
        methods: {
            messagebox :function (rid, k) {
                let that = this;

                console.log(k);

                this.Http('message/deleteMessage',{
                    switch : 'user_delete',
                    rid : rid,
                },function (res) {
                    that.info.splice(k,1)
                })
            },
            getContent : function (rid, mid, x, k) {
                let that = this;
                this.Http('message/content',{
                    rid : rid,
                    mid :mid,
                },function (res) {
                    layer.open({
                        content: res.info.content
                        ,btn: '关闭'
                    });
                    that.info[k].is_readed = 1;
                })
            },
            getIcon:function () {
                let that = this;
                return   units.getHost() + '/public/images/rand/img_img1.png'
            },
            refresh: function (done) {
                new Promise(function (a,b) {
                    setTimeout(function () {
                        done();
                    },500)
                })
            },
            infinite: function (done) {
                let that = this;
                setTimeout(function () {
                    done(true);
                }, 1500)
            },
            formatDateTime: function (str) {
                return units.formatDateTime(str)
            },
            getdata: function (ready=0) {
                let that = this;
                this.Http('message/listd',{
                    ready:ready,
                    switch : 'user',
                    user_id : cookie.get('user_id'),
                },function (res) {
                    if(ready == 0){
                        that.info = res.info;
                    }else{
                        that.ready = res.info;
                    }
                })
            }
        },
        created: function () {
            this.getdata();
            let that = this;
            new Promise(function () {
                that.getdata(1);
            })
            this.$store.state.header.leftShow = false
            cookie.set('curr',2);
        },
        beforeCreate: function () {
            units.title.set('我的消息');
        },
        beforeRouteEnter: function (to, from, next) {
            if(!units.isLogin()){
                layer.msg('请先登录',2,function () {
                    location.href = '#/login';
                })
            }
            next();
        }
    }
</script>
