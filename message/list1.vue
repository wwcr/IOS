<!--页面css样式-->
<style scoped>
    .message {
        background: #f0f4fa;
    }

    .message ul {
        background: #fff;
        margin-bottom: 0.3rem;
    }

    .message ul li {
        margin-left: 0.15rem;
        border-bottom: 1px solid #f1f1f1;
        padding: 0.3rem 0 0.3rem 0.3rem;
    }

    .message ul li .img {
        float: left;
        margin-right: 0.3rem;
        width: 19%;
      position: relative;
    }

    .message ul li .img img {
        width: 1.7rem;
        height: 1.7rem;
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
            <ul v-if="info.length > 0">
                <li v-for="(x,k) in info" @click="href('message/content?id='+x.mid +'&c='+JSON.stringify(x))" v-if="!x.is_readed">
                    <div class="img">
                        <img :src="getIcon()">
                        <i v-if="!x.is_readed"></i>
                    </div>
                    <div class="mess">
                        <h5>{{x.title}}</h5>
                        <p class="p1">{{x.content}}</p>
                        <p class="p2">{{formatDateTime(x.date*1000)}}</p>
                    </div>
                </li>
            </ul>
            <ul>
                <li v-for="(x,k) in ready" @click="href('message/content?id='+x.mid +'&c='+JSON.stringify(x))">
                    <div class="img">
                        <img :src="getIcon()">
                    </div>
                    <div class="mess">
                        <h5>{{x.title}}</h5>
                        <p class="p1">{{x.content}}</p>
                        <p class="p2">{{formatDateTime(x.date*1000)}}</p>
                    </div>
                </li>
            </ul>
        </scroller>
        <navcate></navcate>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    export default {
        name: 'index',
        data () {
            return {
                info: {},
                ready:{},
                icon:['img_img1.png','img_img2.png','img_img3.png','img_img4.png']
            }
        },
        components: {
            navcate
        },
        methods: {
            getIcon:function () {
                let that = this;
                return   units.getHost() + '/public/images/rand/' + that.icon[Math.floor((Math.random()*that.icon.length))]
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
                    ready:ready
                },function (res) {
                    if(ready == 0){
                        that.info = res.info.data;
                    }else{
                        that.ready = res.info.data;
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
        },
        beforeCreate: function () {
            units.title.set('消息');
        },
    }
</script>
