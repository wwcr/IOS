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
        /*margin-bottom: 0.3rem;*/
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
        padding-top: 0.5rem;
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
        /*border-bottom: 1px solid #f1f1f1;*/
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
        /*margin-left: 0.4rem;*/
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
        <div class="resg" v-if="!model" style="padding-top: 1.5rem;">
            <!-- 您已经成功填写需要看护车辆的详细资料，请完成付款，正式启动该服务！ -->
        </div>
        <div class="resg" v-if="model" style="padding-top: 1.5rem;">
            <!-- 请选择寻车服务内容，完成付款开始改服务。 -->
        </div>
        <div class="in_list" v-if="false">
            <ul>
                <li v-for="(x,k) in getServerData">
                    <a>
                        <label>{{k+1}}.{{x.service_text}}</label>
                        <span class=" mess mess_mess" @click="serverClick(k,x)">
                            <img src="../../assets/img/img_18.jpg" v-if="!serverChose[k]">
                            <img src="../../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
                <li>
                    <a class="list">
                        价格：<input type="text" v-model="price" class="text" readonly>元
                    </a>
                </li>
            </ul>
        </div>
        <div class="location">
            <ul style='padding-bottom: .4rem;'>
                <li @click="serverClick(0)">
                    <a>
                        <p>请支付回收费用<span>回收费：¥<i>{{zxprice}}</i></span></p>
                        <!--<span class="loca">-->
                          <!--<img src="../assets/img/img_18.jpg" v-if="!serverChose[0]">-->
                          <!--<img src="../assets/img/cur.jpg" v-else>-->
                        <!--</span>-->
                    </a>
                </li>
                <li @click="serverClick(1)" v-if="false">
                    <a>
                        <p>1. 获得车辆位置，手机报警发送位置<span>服务价格：¥<i>300</i></span></p>
                        <span class="loca">
                          <img src="../../assets/img/img_18.jpg" v-if="!serverChose[1]">
                          <img src="../../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div class="in_list">
            <ul >
                <li>
                    <a>
                        <label><img src="../../assets/img/img_15.png">微信支付</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(0)">
                            <!-- <img src="../assets/img/img_18.jpg" v-if="!choseImg[0]"> -->
                            <!-- <img src="../assets/img/cur.jpg" v-else> -->
                        </span>
                    </a>
                </li>
                <!-- <li>
                    <a>
                        <label><img src="../assets/img/img_17.png">支付宝</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(1)">
                            <img src="../assets/img/img_18.jpg" v-if="!choseImg[1]">
                            <img src="../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label><img src="../assets/img/img_16.png">银行卡</label>
                        <span class="arrow_right"></span>
                        <span class="mess" @click="CpClick(2)">
                            <img src="../assets/img/img_18.jpg" v-if="!choseImg[2]">
                            <img src="../assets/img/cur.jpg" v-else>
                        </span>
                    </a>
                </li> -->
            </ul>
        </div>
         <tips v-if="tips"><!--v-if="tips" -->
            <div class="fixed-ad-img">
                <img src="../../assets/img/order.png">
                <div class="point">
                    <a class="look" @click="href('order/list')">
                        <img src="../../assets/img/order_1.png">
                    </a>
                     <!-- <a class="goon" @click="href('server/content?sid=2')">
                        <img src="../../assets/img/order_2.png">
                    </a> -->
                     <a class="goon" @click="href('order/releasePage')">
                        <img src="../../assets/img/jxadd.png">
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
<script src="//wx.gtimg.com/wxpay_h5/fingerprint2.min.1.4.1.js"></script>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import tips from './../template/popup.vue'
    export default {
        name: 'index',
        data () {
            return {
                chose: false,
                choseImg: [true, false, false],
                currentId: '',
                model: true,
                tips:false,
                price: 300,
                serverChose: [true, false],
                servernum: '1',
                getServerData: {},
                zxprice: 0
            }
        },
        mounted(){
                let order = this.$route.query.order;
                let that = this;
                var set_id = setInterval(function(){
                    that.$http.post(units.domin('order/order_payinfo'), units.params({
                        order: order,
                    })).then(function (res) {
                        if(res.body.code == 2){
                                clearInterval(set_id);
                            //   location.href = '#/server/content';
                            console.log(111)
                            layer.msg(res.data.info, 2, function () {
                                that.tips = !that.tips;
                            })
                                return false;
                        }//该订单已支付
                    });
                    },1000);//           
        },
        methods: {
             goIndex(){
                this.tips = !this.tips;
                location.href = '#/order/list';
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
            getServer: function () {
                this.$http.post(units.host('server'), units.params({
                    type: this.$route.query.type,
                    sw: 'get'
                })).then(function (res) {
                    this.getServerData = res.data.info;
                });
            },
            submit: function () {
                console.log(111)
                let that = this;
                let order = this.$route.query.order;
                if (this.model) {
                    if (parseInt(that.price) <= 0 || !parseInt(that.price)) {
                        layer.msg('订单价格不能少于0元');
                        return false;
                    }
                    if (!that.servernum) {
                        layer.msg('请选择一种服务');
                        return false;
                    }
                }
                layer.loading('请稍等...');
                this.$http.post(units.domin('pay/wechat_pay'), units.params({
                    type: that.currentId,
                    order: order,
                    price: that.price,
                    serviceType: cookie.get('serviceType'),//那种服务区分,
                    server: that.servernum,//如果有服务类别,用户勾选的服务
                })).then(function (res) {
                    layer.loading(false);
                    console.log(res);
                    // that.href(res.data.mweb_url);
                    // window.open(res.data.mweb_url);
                     window.location.href = res.data.mweb_url;
                    // if (res.data.code > 0) {
                    //     layer.msg(res.data.info, 2, function () {
                    //         // that.href('carnurse/success?id=' + that.$route.query.type)
                    //     })
                    // } else {
                    //     layer.msg(res.data.info)
                    // }
                });
            }
        },
        created: function () {
            this.curInit();
            this.CpClick(0);
            units.title.set('支付')
            if (this.$route.query.type == 2) {
                this.model = true;
                this.getServer();
            } else {
                this.model = false;
            }
            this.$store.state.header.left = function () {
                location.href = '#/order/list';
            };
            this.zxprice = this.$route.query.price
        },
        components: {
            tips
        }
    }
    
</script>
