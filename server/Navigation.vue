<!--页面css样式-->
<style scoped>
    .banner{
        width: 100%;
    }
    .banner img{
        width: 100%;
        height: 5.14rem;
    }
    .center{
        background: #fff;
        width: 90%;
        border-radius: 5px;
        margin: 0 auto;
        margin-top:1rem; 
        padding: 0.3rem;
        -moz-box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.2);
        -webkit-box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.2);
        box-shadow:4px 4px 12px 4px rgba(20%,20%,40%,0.1);
        position: relative;
        top: -0.5rem;
    }
    .center p span{
        color: #1e1e1e;
        font-size: 0.4rem;
        height: 1rem;
        line-height: 0.6rem;
        width: 90%;
        float: left;
        margin-top: 0.2rem;
    }
    .center p img{
        width: 0.6rem;
        height: 0.6rem;
        float: left;
        vertical-align: middle;
        margin-top: 0.2rem;
        margin-right: 0.2rem;
    }
    .nav{
        text-align: center;
        margin-top: 3rem;
    }
    .nav img{
        width: 5.4rem;
    }
    .tion{
        padding-top:1.6rem;
    }
</style>
<!--导航前往-->
<template>
    <div class="tion">
        <div class="banner">
            <img v-bind:src="pic">
        </div>
        <div class="center clearfix">
            <p><img src="../../assets/img/img_34.png"><span>拍照时间：{{car_addtime}}</span></p>
            <p><img src="../../assets/img/img_33.png"><span>发现位置：{{car_location}}</span></p>
        </div>
        <div class="nav">
            <a class="mode" @click.stop="href('server/map')"><img src="../../assets/img/img_35.png"></a>
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
                currentNum: 1,
                sid: '',
                search: false,
                status: 1,
                searchKeyword: '',
                show: true,
                count: '',
                timer: null,
                car_addtime:'',
                car_location:'',
                pic:'',
            }
        },
        mounted(){
            let id = this.$route.query.id;
            console.log(this.$route.query.id)
            this.$http.post(units.host('get_finded_pic','api'), {
                    id: id//穿车牌
                }).then(function (res) {
                    console.log(res)
                    this.car_addtime = res.body.car_addtime;
                    this.car_location = res.body.car_location;
                    this.pic = units.getHost() + res.body.car_photo;
                    console.log(this.pic);
                    // console.log(units.getHost());
                });
           
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
                    that.moreThat = false;
                })
            }
        },
        methods: {
            gotorun:function (x) {
                console.log(x);
                location.href = '#/server/details?cid='+x.find_id;
            },
            
        },
        created () {
            this.$store.state.header.left = function () {
                location.href = '#/server/content?cur=2';
            };
        }
}
</script>
