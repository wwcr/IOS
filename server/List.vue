<!--页面css样式-->
<style scoped>
    .con_top{
        padding:0.4rem;
        background: #fff;
    }
    .con_l{
        width: 50%;
        float: left;
        padding-top: 0.6rem;
    }
    .con_l .p1{
        font-size: 0.5rem;
        color: #1e1e1e;
        display: block;
        font-weight: 100;
        height: 1rem;
        line-height: 1rem;
    }
    .con_l .p2{
        color: #999;
        font-size: 0.4rem;
        height: 1rem;
        line-height: 1rem;
    }
    .con_r{
        width: 50%;
        float: right;
        text-align: right;
    }
    .con_r img{
        width: 4rem;
        height: 3rem;
    }
    .con_list{
        width: 100%;
        margin-top: 0.3rem;
    }
    .con_list ul li:first-child{
        background: #5992f1;
        color: #fff;
    }
    .con_list ul li{
        border-bottom:1px solid #c7d3e5;
        height: 1.3rem;
        line-height: 1.3rem;
        text-align: center;
        width: 100%;
        background: #fff;
        color: #1e1e1e;
        font-size: 0.4rem;
    }
    .con_list ul li p{
        display: inline-block;
        float: left;
        width: 33%;
    }
    .con_list ul li p a{
        color: #e65e5e;
    }
</style>
<!--服务列表-->
<template>
    <div class="con_tent">
        <div class="con_top clearfix">
            <div class="con_l">
                <p class="p1">车牌号码：{{info.card_number}}</p>
                <p class="p2">看护时间：{{len(info.card_addtime)}}</p>
            </div>
            <div class="con_r">
                <img src="../../assets/img/img_13.jpg">
            </div>
        </div>
        <div class="con_list clearfix">
            <ul>
                <li>
                    <p>时间</p>
                    <p>位置</p>
                    <p>详情</p>
                </li>
                <li>
                    <p>2017-01-01</p>
                    <p>北京是朝阳区</p>
                    <p><a href="/server/navigation">查看</a></p>
                </li>
                <li>
                    <p>2017-01-01</p>
                    <p>北京是朝阳区</p>
                    <p><a>查看</a></p>
                </li>
                <li>
                    <p>2017-01-01</p>
                    <p>北京是朝阳区</p>
                    <p><a>查看</a></p>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                info:{}
            }
        },
        methods: {
            len:function (str) {
                return str.substring(0,10);
            },
            getdata:function () {
                this.$http.post(units.host('server'),units.params({
                    id:this.$route.query.id,
                    sid:this.$route.query.sid,
                    sw:'list'
                })).then(function (res) {
                    this.info = res.data.info;
                });
            }
        },
        created: function () {
            this.getdata()
        },
        beforeCreate:function () {},
    }
</script>