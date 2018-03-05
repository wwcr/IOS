
<!--页面css样式-->
<style scoped lang='scss'>
    @import "../../../static/mobiscroll/css/mobiscroll.jquery.min.css";
    
    .resg {
        background: #f0f4fa;
        font-size: 0.36rem;
        line-height: 0.6rem;
        padding: 0.52rem 0.38rem;
        color: #787878;
    }

    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }

    .in_list li {
        // height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
    }

    .in_list li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        padding: .3rem 0;
        // height: 1.49rem;
        // line-height: 1.49rem;
        // min-height: 1.49rem;
    }
    .in_list-gps li a {
        display: flex;
        align-items: center;
        padding: 0.48rem 0;
        .message{
            margin-left: .8rem;
        }

    }
    .in_list li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
    }


    .in_list .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        // margin-top: 0.05rem;
        -webkit-tap-highlight-color: transparent;
        // font-family: "微软雅黑";
        // font-family: 'Droidsansfallback';
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }


    .file {
        // height: 3rem;
        opacity: 0;
        width: 100%;
    }
    //提交按钮
    .sub_btn {
        background: #f0f4fa;
    }
    //车辆佣金
    .in_list1{
        font-size: .47rem;
        background: #fff;
        margin-top:.2rem;
        .car-price{
            padding: 0 .6rem;
            border-top: .2rem solid #edf1f6;
            div{
                padding: .48rem 0;
                a{
                    color: #000;
                    .message{
                        margin-left: .8rem;
                        font-size: .45rem;
                        position: relative;
                        top: -.05rem;
                    }
                }
            }
        }
    }
    //本次建议价
    .test-text{
        background: #f0f4fa;
        color: #fc5b5c;
        padding: .4rem .4rem .05rem .4rem;
        font-weight: 500;
    }
    

    .in_list li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
    }
    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 67%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        // line-height: 1.48rem;
        display: inline-block;
    }

    .in_list .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        // margin-top: 0.05rem;
        -webkit-tap-highlight-color: transparent;
        font-family: "微软雅黑";
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }


    .arrow_right_text{
        float: right;
        color: #2c7dfe;
        font-size: .4rem;
        padding-right: .5rem;
        position: relative;
        top: .28rem;
    }
    .gps-page{
        margin-top: .3rem;
    }
</style>
<!--平台执行-->
<template>
    <div id="Terrace" style='padding-top: 1.25rem;' v-if='find_car_val'>
        <div class="resg">
            请如实填写需要寻找车辆信息，本平台只提供寻车服务，该信息不做它用，请放心上传！
        </div>
        <div class="in_list">
            <ul class="in_list">
                <li>
                    <a>
                        <label>所在位置</label>
                        <span @click='carCity'>
                            <span 
                                class="message"
                                style="position:relative;top: .18rem;width: 73%;">
                            <input 
                                unselectable="on" 
                                onfocus="this.blur()" 
                                readonly 
                                type="text" 
                                v-model="form.card_location" 
                                class="text"
                                placeholder="请选择所在位置">
                            </span>
                        </span>
                    </a>
                </li>
                <li class="price">
                    <a>
                        <label>合同金额</label>
                        <span class="arrow_right_text">万元</span>
                        <span 
                            class="message" 
                            style="width: 60%; position: relative; top: .21rem;">
                            <input 
                                type="text" 
                                v-model="form.contract_money" 
                                class="text" 
                                placeholder="请输入合同金额" 
                                v-on:blur="countMoney()">
                        </span>
                    </a>
                </li>
                <li class="price">
                    <a>
                        <label>回收期限</label>
                        <span class="arrow_right_text">天数</span>
                        <span 
                            class="message" 
                            style="width: 60%; position: relative; top: .21rem;">
                            <input
                                type="text" 
                                v-model="form.card_contract" 
                                class="text" 
                                placeholder="请输入回收期限天数" >
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>G&nbsp;&nbsp;&nbsp;P&nbsp;&nbsp;&nbsp;S</label>
                        <span @click='gpsFn'>
                            <span 
                                class="message"
                                style="position:relative;top: .21rem;width: 73%;">
                            <input 
                                unselectable="on" 
                                onfocus="this.blur()" 
                                readonly 
                                type="text" 
                                v-model="form.card_gps" 
                                class="text"
                                placeholder="请选择是或否">
                            </span>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
         <!-- 有GPS信息 -->
        <div class="gps-page" v-show = 'gpsShow'>
            <ul class="in_list in_list-gps">
                <li>
                    <a>
                        <label>GPS平台</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input  
                            type="text" 
                            v-model="gps.platform" 
                            class="text" 
                            style="width: 100%;"
                            placeholder="请输入所使用的GPS平台">
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>账&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;号</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input  
                            type="text" 
                            v-model="gps.user" 
                            class="text" 
                            placeholder="请输入GPS平台账号">
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>密&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;码</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input  
                            type="text" 
                            v-model="gps.pwd" 
                            class="text" 
                            placeholder="请输入GPS平台密码">
                        </span>
                    </a>
                </li>
            </ul>
        </div>

        <div class="in_list1">
            <div class="car-price">
                <div>
                    <a>
                        <label>车辆佣金</label>
                        <span class="message">
                            <input 
                                type="text" 
                                v-model="form.card_price" 
                                placeholder="请输入车辆佣金" 
                                style="width: 4.2rem"
                                class="text">
                        </span>
                    </a>
                </div>
            </div>
            <div class="test-text">
                <span v-if="form.suggest_money > 0.8">
                    本次建议价: <span>0.80</span>  <span> - {{form.suggest_money.toFixed(2)}}</span> 万元
                </span>
                <span v-if="form.suggest_money < 0.8 && form.suggest_money>0">
                    本次建议价: <span>0.80</span>万元
                </span>
                <span v-if="form.suggest_money == 0 && !form.card_money">
                    本次建议价: <span>0</span>万元
                </span>
            </div>
        </div>
        <div class="sub_btn">
            <a @click="postData()">提&nbsp;&nbsp;&nbsp;&nbsp;交</a>
        </div>
        <!-- 城市 -->
        <Province
            v-show= 'proFlag'
            @closePro='closePro'
            :ProList='ProList'/>
        <!-- 是否GPS -->
        <GpsPicker
            v-if='gpsFlag'
            @closePicker= 'closePicker'
        />
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import scroll from '../../../static/mobiscroll/js/mobiscroll.jquery.min'
    import Province from '@/components/VehicleEvaluation/children/City/province'
    import GpsPicker from '@/components/frame/gpsPicker'
    export default {
        name: 'Terrace',
        data () {
            return {
                info: {},
                time: '',
                proFlag: false,
                selectFlag: false,
                ProList: [], //省份数据
                find_car_val: {},
                form: {
                    card_price: '',//车辆佣金
                    card_money: '',//合同金额
                    card_contract: '',//回收期限,
                    card_gps: '否',
                    card_location: '', //所在位置
                    suggest_money: 0
                },
                gps: {
                    platform: '',
                    user: '',
                    pwd: ''
                },
                gpsShow: false,//是否显示gps信息
                gpsFlag:false,//是否显示gps弹窗
                gpsVal: ''//gps值
            }
        },
        methods: {
            gpsFn () {//选择是否GPS
               this.gpsFlag = true
                              
            },
            closePicker (obj) {//关闭GPS
                    if( obj.id == 0 ){ //取消
                        this.form.gps = '';
                    }else{ //确定
                        this.form.card_gps = obj.gps;
                        if(obj.gps == '是'){
                            this.gpsShow = true;
                            this.form.suggest_money = (this.form.contract_money) * 0.2
                        }else{
                            this.gpsShow = false;
                            this.form.suggest_money = (this.form.contract_money) * 0.3
                        }
                        this.form.suggest_money =  this.form.suggest_money
                    }
                    this.gpsFlag = false
            },
            countMoney () {
                if (this.form.card_gps == '是') {
                    this.form.suggest_money = (this.form.contract_money) * 0.2
                } else {
                    this.form.suggest_money = (this.form.contract_money) * 0.3
                }
                this.form.suggest_money =  this.form.suggest_money
                
            },
            carCity () {//获取城市数据
                this.$http.post(units.host('provincetest', 'api')).then( function (res) {
                    if (res.ok) {
                        this.ProList = res.body
                        this.proFlag = true
                    }
                })
            },
            closePro (obj) {//关闭省份弹出框
                // console.log(obj)
                this.proFlag = false
                this.form.card_location = obj.city.cityName
                // this.form.card_city = obj.city.cityName
                // this.form.pro_num = obj.city.proID
                // this.form.city_num = obj.city.cityID
            },
            validate: function (fn, midia) {
                let flag = true;
                // let midia = $('input').not('.gps-page input');
                console.log(midia.eq(0).attr('placeholder'))
                let len = midia.length;
                for (var i = 0; i < len; i++) {
                    if (!midia.eq(i).val()) {
                        let tips = midia.eq(i).attr('placeholder');
                        layer.msg(tips);
                        flag = false;
                        break;
                    }
                }
                fn && fn(flag);
            },
            postData: function () {
                let that = this;
                if(this.gpsShow){ //判断gps是否有
                    this.validate(function (ress) {
                        if (ress) {
                            that.requestData()
                        }
                    }, $('input'))
                }else {
                    this.validate(function (ress) {
                        if (ress) {
                            that.requestData()
                        }
                    }, $('input').not('.gps-page input'))
                }
                
            },
            requestData () {
                that.Http('order/terrace', {
                    ex_term: that.form.card_contract,
                    ex_money: that.form.card_price,
                    ex_fid: that.find_car_val.find_id,
                    ex_overdue: 1,
                    ex_virecord: '是',
                    ex_gps: that.form.card_gps,
                    ex_location: that.find_car_val.card_city,
                    ex_brand:that.find_car_val.card_brand,
                    gps_platform: that.gps.platform,
                    gps_user: that.gps.user,
                    gps_pwd: that.gps.pwd,
                }, function (res) {
                    layer.loading(false);
                    if (res.code > 0) {
                        that.href('order/pay?order='+res.info+'&price='+that.form.card_price)
                    } else {
                        layer.msg(res.msg)
                    }
                })
            }
        },
        components: {
            Province,
            GpsPicker
        },
        created () {
            let that = this
            this.form.ex_fid = this.$route.query.id;
            // this.form.brand_num = cookie.get('brand_num')
            this.form.brand_num = this.$route.query.carId
            // console.log(this.form.brand_num)
            this.Http('order/query_find', {
                id:that.form.ex_fid
            }, function (res) {
                // console.log(res)
                that.find_car_val = res.info
            })
        },
        beforeCreate: function () {
            units.title.set('发布订单');
        }
    }
</script>
