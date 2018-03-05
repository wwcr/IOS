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
    <div class="details">
        <div class="center">
            <div class="list">
                <p>车&#12288;&#12288;型：<span>{{finds.card_brand}}-{{finds.card_model}}</span></p>
                <p>车辆归属地：<span class="blue">{{finds.card_city}}</span></p>
                <p>车牌号码：<span class="orange">{{finds.card_number}}</span></p>
                <!-- <p>车辆颜色：<span>{{finds.card_color}}</span></p> -->
                <p>车辆状态：
                    <span class="orange" v-if="finds.car_status == 1">查找中</span>
                    <span class="orange" v-if="finds.car_status == 2">确认中</span>
                    <span class="orange" v-if="finds.car_status == 3">已找到</span>
                </p>
                <p>发布时间：<span>{{finds.card_addtime}}</span></p>
                <div v-if="false">
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
            </div>
            <div class="list" v-if="false">
                <p>违章内容：<span>无</span></p>
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
                finds:{},
            }
        },
        components: {
            tips
        },
        methods: {
            getlist: function () {
                let that = this;
                that.Http('find/serverDetails', {
                    id: that.$route.query.cid
                }, function (res) {
                    that.finds = res.info;
                })
            },
            getCard:function () {}
        },
        created: function () {
            units.title.set('车辆信息');
            this.getlist();
        },
        mounted: function () {
        }
    }
</script>
