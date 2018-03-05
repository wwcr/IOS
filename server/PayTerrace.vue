<!--页面css样式-->
<style scoped>
    .resg {
        background: #f2f6f7;
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.52rem 0.38rem;
    }

    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
        margin-bottom: 0.3rem;
    }

    .in_list li {
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
    }

    .in_list li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        height: 1.49rem;
        line-height: 1.49rem;
        min-height: 1.49rem;
    }

    .in_list li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
    }

    .in_list li a label img {
        width: 0.48rem;
        height: 0.48rem;
        vertical-align: middle;
        margin-top: -0.05rem;
        margin-right: 0.33rem;
    }

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 70%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        line-height: 1.48rem;
        display: inline-block;

    }

    .in_list .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        margin-top: 0.05rem;
        -webkit-tap-highlight-color: transparent;
        /* font-family: "微软雅黑"; */
        /* font-family: 'Droidsansfallback'; */
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }

    .mess {
        float: right;
        width: 60%;
        height: 100%;
        padding-top: 0.55rem;
    }

    .mess_mess {
        width: 10%;
    }

    .mess img {
        width: 0.36rem;
        height: 0.36rem;
        float: right;
    }

    .cur img {
        width: 0.36rem;
        height: 0.36rem;
    }

    .in_list li a.list {
        font-size: 0.48rem;
        color: #1e1e1e;
    }

    .in_list li a.list .text {
        width: 2rem;
        height: 0.9rem;
        border: 1px solid #f1f1f1;
        margin-right: 0.3rem;
        margin-top: 0.3rem;
        text-indent: 0.2rem;
    }

    .location {
        background: #fff;
    }

    .location ul li {
        height: 2rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
        padding-top: 0.35rem;
    }

    .location ul li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
    }

    .location ul li a p {
        font-size: 0.48rem;
        color: #1e1e1e;
        width: 80%;
        display: inline-block;
    }

    .location ul li a p span {
        display: block;
        margin-left: 0.4rem;
    }

    .location ul li a p span i {
        color: #f05c27;
        font-weight: 600;
        font-style: normal;
        margin-left: 0.1rem;
    }

    .loca {
        float: right;
        margin-top: 0.5rem;
    }

    .loca img {
        width: 0.36rem;
        height: 0.36rem;
        float: right;
    }
</style>
<template>
    <!--付款页面-->
    <div class="pay">
        <div class="resg">
            请支付执行费用押金
        </div>
        <div class="location">
            <ul>
                <li>
                    <a>
                        <p>
                            执行费：¥
                            <b>{{payOrder}}</b>
                            元
                        </p>
                    </a>
                </li>
            </ul>
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <label><img src="../../assets/img/img_15.png">微信支付</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(0)">
                            <img src="../../assets/img/img_18.jpg" v-if="!choseImg[0]">
                            <img src="../../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label><img src="../../assets/img/img_17.png">支付宝</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(1)">
                            <img src="../../assets/img/img_18.jpg" v-if="!choseImg[1]">
                            <img src="../../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label><img src="../../assets/img/img_16.png">银行卡</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(2)">
                            <img src="../../assets/img/img_18.jpg" v-if="!choseImg[2]">
                            <img src="../../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <tips v-if="tips">
            <div class="fixed-ad-img">
                <img src="../../assets/img/order.png">
                <div class="point">
                    <a class="look" @click="href('order/list')">
                        <img src="../../../src/assets/img/order_1.png">
                    </a>
                    <a class="goon" @click="href('server/content?sid=2')">
                        <img src="../../../src/assets/img/order_2.png">
                    </a>
                </div>
                <div class="close-fixed-ad" @click="goIndex()"></div>
            </div>
        </tips>
        <div class="sub_btn">
            <a @click="submit">提交</a>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import tips from '../template/popup.vue'
    export default {
        name: 'index',
        data () {
            return {
                chose: false,
                choseImg: [true, false, false],
                currentId: '',
                model: true,
                price: 300,
                serverChose: [true, false],
                servernum: '1',
                getServerData: {},
                tips:false,
                payOrder:0
            }
        },
        components: {
            tips
        },
        methods: {
            goIndex(){
                this.tips = !this.tips;
                location.href = '#/';
            },
            serverClick: function (id) {
                this.serverChose = [];
                for (let i = 0; i < 2; i++) {
                    this.serverChose.push(false);
                }
                this.serverChose[id] = true;
            },
            CpClick: function (id) {
                this.curInit();
                this.choseImg[id] = true;
                this.currentId = id;
            },
            curInit: function () {
                this.choseImg = [];
                for (let i = 0; i < 3; i++) {
                    this.choseImg.push(false);
                }
            },
            getPrice:function () {
                let that = this;
                this.Http('order/getPayorder',{
                    order:that.$route.query.order
                },function(res){
                    if(res.code > 0){
                        that.payOrder = res.info.order_price/100;
                        that.price = that.payOrder;
                    }else{
                        layer.msg(res.msg)
                    }
                })
            },
            submit: function () {
                let that = this;
                let order = this.$route.query.order;
                if(!order){
                    layer.msg('订单号有误,支付失败');
                    return false;
                }
                layer.loading('请稍等...');
                this.$http.post(units.domin('order/payorder'), units.params({
                    type: that.currentId,
                    order: order,
                    price: that.price,
                    serviceType: cookie.get('serviceType'),//那种服务区分,
                    server: that.servernum,//如果有服务类别,用户勾选的服务
                })).then(function (res) {
                    layer.loading(false);
                    if (res.data.code > 0) {
                        layer.msg(res.data.info, 2, function () {
                            that.tips = !that.tips;
                        })
                    } else {
                        layer.msg(res.data.info)
                    }
                });
            }
        },
        created: function () {
            this.curInit();
            this.CpClick(0);
            this.getPrice();
            units.title.set('支付');
            this.$store.state.header.left = function () {
                location.href = '#/';
            };
        }
    }
</script>
