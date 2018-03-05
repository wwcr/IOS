<template>
    <div class="vehicle-evaluation-page">
        <div class="assess-end">
            <div>
                <p class="assess-title">您的车辆预评估</p>
                <p class="assess-price"><b>{{sum}}</b><small>万</small></p>
            </div>
        </div>
        <ul class="vehicle-evaluation-ul">
            <li>
                <a>
                    <label>车辆品牌</label>
                    <span>
                        <span class="arrow_right"></span>
                        <span class="message">
                            <input 
                                unselectable="on" onfocus="this.blur()"
                                @click="carBrand()"
                                readonly   
                                type="text" 
                                v-model="form.card_brand" 
                                class="text"
                                placeholder="请选择车辆品牌">
                        </span>
                    </span>
                </a>
            </li>
            <li>
                <a>
                    <label>所在城市</label>
                    <span @click="carCity()">
                        <span class="arrow_right"></span>
                        <span class="message">
                            <input 
                                unselectable="on" onfocus="this.blur()"
                                readonly  
                                type="text" 
                                v-model="form.card_city" 
                                class="text"
                                placeholder="请选择所在城市">
                        </span>
                    </span>
                </a>
            </li>
            <li>
                <a>
                    <label>上牌时间</label>
                    <span @click="carStartDate()">
                        <span class="arrow_right"></span>
                        <span class="message">
                            <input 
                                unselectable="on" onfocus="this.blur()"
                                readonly  
                                type="text" 
                                v-model="form.time" 
                                class="text"
                                placeholder="请选择上牌时间">
                        </span>
                    </span>
                </a>
            </li>
            <!-- <li>
                <a>
                    <label>购买价格</label>
                    <span class="arrow_right_only">万元</span>
                    <input
                        type="text" v-model="form.card_money" 
                        class="text-write"
                        style="color:#b4b4b4"
                        placeholder="请输入价格"
                        >
                </a>
            </li>
            <li>
                <a>
                    <label>行驶里程</label>
                    <span class="arrow_right_only">万公里</span>
                    <input
                        type="text" v-model="form.card_mileage" 
                        class="text-write" 
                        placeholder="请输入公里数"
                        style="color:#b4b4b4"
                        >
                </a>
            </li> -->
              <li class="mileage">
                    <a>
                    <label>行驶里程</label>
                    <span class="arrow_right_text">万公里</span>
                    <span class="message" style="width: 58%;margin-left: .25rem;">
                        <input type="number" v-model="form.card_mileage" class="text" placeholder="请输入行驶里程">
                    </span>
                </a>
            </li>
            <li class="price">
                <a>
                    <label>购买价格</label>
                    <span class="arrow_right_text">万元</span>
                    <span class="message" style="width: 62.5%;margin-left: .25rem;">
                        <input type="number" v-model="form.card_money" class="text" placeholder="请输入购买价格">
                    </span>
                </a>
            </li>
        </ul>
        <div  class="query-btn-box"><button class="query-btn" @click='startAssess'>开始评估</button></div>
        <!-- 车型 -->
        <listInfo 
            :brandList='brandList'
            @closeBrand = 'closeBrand'
            ref='detailInfo'
            v-show = 'infoFlag'/>
        <!-- 城市 -->
        <Province
            v-show= 'proFlag'
            @closePro='closePro'
            :ProList='ProList'/>
        <!-- 时间 -->
        <dataTime
            v-show='timeFlag'
            @closeData='closeData'/>
    </div>
</template>
<script>
import units from '@/tools/units'
import listInfo from '@/components/frame/indexList'
import Province from '@/components/VehicleEvaluation/children/City/province'
import dataTime from '@/components/frame/dataTime'
export default {
    name: '',
    data () {
        return {
            infoFlag: false,//车牌信息
            proFlag: false,
            timeFlag: false,
            cardata:{},
            sum: 0,
            brandList: [], //车牌数据
            ProList: [], //省份数据
            form: {
                card_brand: '', //车辆品牌
                card_money: '',//购买价格
                card_mileage: '',//里程
                card_city: '',//所在城市,
                brand_num: '',//车型标识，
                pro_num:'',//省份标识
                city_num:'',//城市标识
                time: '',//时间
                month: '', //月份
                year: '',//年

            }
        }
    },
    beforeRouteLeave (to, from, next) {
        if( this.infoFlag || this.proFlag) {
            this.infoFlag = false//关闭品牌弹窗
            this.proFlag = false//关闭城市弹窗
            next(from.path)
        } else {
            next()
        }
    },
    methods: {
        startAssess () {//评估
            let {
                brand_num,
                card_money,
                card_mileage,
                pro_num,
                city_num,
                year,
                month
            } = this.form
            this.$http.post(units.host('assess', 'api'), {
                city: city_num,
                province: pro_num,
                car: brand_num,
                useddate: year,
                useddateMonth: month,
                mileage: card_mileage,
                price: card_money
            }).then(function (res) {
                if (res.ok) {
                    if(typeof (res.body) =='string'){
                        alert('输入参数有误')
                    } else {
                         this.sum = res.body.est_price_result[1]
                    }
                    // console.log(res)
                }
            });
        },
        carBrand (url) { //车辆品牌
            this.infoFlag = true
            this.getData(url)
        },
        carStartDate () {//上牌时间
            console.log('上牌时间')
            this.timeFlag = true
        },
        carCity () {//获取城市数据
            this.$http.post(units.host('provincetest', 'api')).then(function (res) {
                if (res.ok) {
                    this.ProList = res.body
                    console.log(res)
                    this.proFlag = true
                }
            });
        },
        closeBrand (val) { //关闭车辆品牌弹出框
            this.infoFlag = false
            this.form.card_brand = val.cxname
            this.form.brand_num = val.id
        },
        closePro (obj) {//关闭省份弹出框
            console.log(obj)
            this.proFlag = false
            this.form.card_city = obj.city.cityName
            this.form.pro_num = obj.city.proID
            this.form.city_num = obj.city.cityID
        },
        closeData (time) {//关闭日期弹出框
            if(time) {
                this.form.year = time.getFullYear()
                this.form.month = time.getMonth()+1 
                this.form.time = `${this.form.year}年${this.form.month}月`
            }
            // alert('取消')
            this.timeFlag = false
        },
        getData (url) { //获取车辆品牌数据
            this.$http.post(units.host('brandtest', 'api')).then(function (res) {
                if (res.ok) {
                    this.brandList = res.body
                }
            });
        }
    },
    created () {
        // console.log(num.formatMoney())
        units.title.set('车辆评估');
        // this.getData()
    },
    components: {
        listInfo,
        Province,
        dataTime
    }
}
</script>
<style scoped lang='scss'>
    .vehicle-evaluation-page{
        width: 100%;
        box-sizing: border-box;
        padding-top:1.25rem; 
        background: #f0f4fa;
        font-size: .4rem;
        .assess-end{
            box-sizing: border-box;
            margin-top:.4rem; 
            padding: 0 .4rem;
            height: 3rem;
            border-radius: .5rem;
            text-align: center;
            div{
                width: 100%;
                height: 100%;
                background: #fff;
                .assess-title{
                    padding-top:.7rem; 
                    font-size: .4rem;
                    color: #1e1e1e;
                }
                .assess-price{
                    margin-top:rem; 
                    margin-bottom:.5rem; 
                    color: #3d87ff;
                    b{
                        font-size: .7rem;
                    }
                    small{
                        margin-left:.1rem;
                    }
                }
            }
        }
    }
    .vehicle-evaluation-ul {
        margin-top:.4rem; 
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }

    .vehicle-evaluation-ul li {
        // height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
        padding: .4rem 0;
    }

    .vehicle-evaluation-ul li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        // height: 1.49rem;
        // line-height: 1.49rem;
        // min-height: 1.49rem;
    }

    .vehicle-evaluation-ul li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
        position: relative;
        top: .01rem;
    }

    .vehicle-evaluation-ul .message {
        position: relative;
        float: right;
        margin: 0;
        // height: auto;
        width: 70%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #b4b4b4;
        font-size: 0.48rem;
        // line-height: 1.48rem;
        display: inline-block;
    }

    .vehicle-evaluation-ul .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        margin-top: 0.05rem;
        -webkit-tap-highlight-color: transparent;
        // font-family: 'Droidsansfallback';
        // font-family: "微软雅黑";
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
        position: relative;
        top: .05rem;
    }

    .vehicle-evaluation-ul li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        // height: 1.48rem;
        background: url(../../assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }
     .vehicle-evaluation-ul li a .arrow_right_only {
        position: relative;
        display: block;
        width: 1.3rem;
        // height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
        color: #b4b4b4;
    }

    .vehicle-evaluation-ul li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.5rem;
        // height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }
    .query-btn-box{
        padding: 0 .4rem;
        background: #f0f4fa;
        font-size: .4rem;
        color: #fff;
        width: 100%;
        height: 1.2rem;
        border-radius: .2rem;
        margin-top:1.2rem;
        .query-btn{
            width: 100%;
            height: 100%;
            border-radius: .2rem;
            border: 0;
            outline: none;
            background: url('../..//assets/img/btn-bg.png') no-repeat;
            background-size: cover;
        }
    }
    .text-write{
        margin-left:.5rem;
    }
    .text{
        color: #000;
    }


        #select{
        position: absolute;
        width:5.3rem;
        top:1.3rem;
        left:0rem;
        background: #fff;
        border: .01rem solid #f0f4fa;
        li{
            border-bottom: .01rem solid #f0f4fa;
            height:1rem;
            line-height: 1rem;
            padding: 0 .3rem;
        }
    }
    .license-title{
        font-size: .48rem;
        padding-bottom:.4rem; 
    }
    #Findcar{
        padding-top:1.25rem; 
    }
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

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 65%;
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
        font-family: "微软雅黑";
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }

    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background: url(../../assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a .arrow_right_only {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .arrow_right_text{
        float: right;
        color: #2c7dfe;
        font-size: .4rem;
        position: relative;
        top: .1rem;
    }

    .in_list li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .pledge {
        margin-top: 0.3rem;
        background: #fff;
        padding: 0.4rem;
    }

    .picture {
        border: 1px dashed #bcc6d6;
        margin-bottom: 0.3rem;
        text-align: center;
        position: relative;
        background-size: 20%;
        overflow: hidden;
        display: flex;
        flex-wrap: wrap;
        padding-bottom:.3rem; 
        padding-right:.3rem; 
        div{
            background: url(../../assets/img/license_bg.png) no-repeat center;
            background-size: 100%;
            width: 2.1rem;
            height: 2.1rem;
            margin-top: .3rem;
            margin-left:.3rem; 
            input{
                width:100%;
                height: 100%;
            }
            .file{
                width:100%;
                height: 100%;
                font-size: .01rem;
                opacity: 0;
            }
        }
        
    }

    .borrow {
        border: 1px dashed #bcc6d6;
        margin-bottom: 0.3rem;
        text-align: center;
        position: relative;
        background-size: 20%;
        overflow: hidden;
        display: flex;
        flex-wrap: wrap;
        padding-bottom:.3rem; 
        padding-right:.3rem;
        div{
            background: url(../../assets/img/license_bg.png) no-repeat center;
            background-size: 100%;
            width: 2.1rem;
            height: 2.1rem;
            margin-top: .3rem;
            margin-left:.3rem; 
            input{
                width:100%;
                height: 100%;
            }
            .bow_file{
                width:100%;
                height: 100%;
                font-size: .01rem;
                opacity: 0;
            }
        }
    }

    .picture img {
        // width: 100%;
        /*height: 3rem;*/
        // text-align: center;
        // position: absolute;
        width: 2.1rem;
        height: 2.1rem;
        text-align: center;
        position: absolute;
        top:0.3rem;
        left:0.3rem;
        /*width: 1.88rem;*/
        /*height: 1.23rem;*/
        /*text-align: center;*/
        /*position: absolute;*/
        /*top: 31%;*/
        /*left: 40%;*/
    }

    .borrow img {
        width: 2.1rem;
        height: 2.1rem;
        text-align: center;
        position: absolute;
        top:0.3rem;
        left:0.3rem;
    }

    .aptitude {
        color: #787878;
        font-size: 0.3rem;
        line-height: 0.48rem;
        margin-top: 0.5rem;
    }

    .pact {
        color: #F05C27;
        font-size: 0.3rem;
        margin-top: 0.24rem;
    }

    .fixed-ad-layer {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 1000;
        background: rgba(0, 0, 0, .8);
        -webkit-transform: translate3D(0, 0, 0);
        transform: translate3D(0, 0, 0);
    }

    .fixed-ad-layer .fixed-ad-con {
        width: 300px;
        margin: 0 auto;
        position: absolute;
        left: 50%;
        top: 50% !important;
        -webkit-transform: translateY(-50%);
        transform: translateY(-50%);
        margin-left: -150px;
    }

    .fixed-ad-layer .fixed-ad-con .fixed-ad-img {
        display: block;
        text-align: center;
        max-width: 300px;
        height: auto;
        position: relative;
    }

    .fixed-ad-layer .fixed-ad-con .fixed-ad-img img {
        max-width: 100%;
        height: auto;
    }

    .close-fixed-ad {
        position: relative;
        width: 14px;
        height: 14px;
        bottom: 0px;
        z-index: 2;
        background: url(../../assets/img/xxxx.png);
        background-size: cover;
        left: 50%;
        margin-left: -18px;
        margin-top: 30%;
        cursor: pointer;
    }

    .p1 {
        position: absolute;
        top: 48%;
        color: #fff;
        font-size: 0.7rem;
        left: 37%;
    }

    .p2 {
        position: absolute;
        color: #787878;
        bottom: 0.9rem;
        font-size: 0.38rem;
        line-height: 0.8rem;
        padding: 0 0.9rem;
    }
    
    .in_list1{
        font-size: .47rem;
        background: #fff;
        margin-top:.2rem;
        .time-city{
            border-bottom: .01rem solid #cfd7e6;
            box-sizing: border-box;
            line-height: 1.3rem;
            display: flex;
            justify-content: space-between;
            .li{
                width: 100%; 
                padding: 0 .42rem;
                border-right: .01rem solid #cfd7e6;
                display: flex;
                justify-content: space-between; 
                input{
                    width:1.8rem;
                    height: 80%;
                    position: relative;
                    top: .14rem;
                }
                img{
                    width: .4rem;
                    position: relative;
                    top: -.1rem;
                }
            }
        }
    }
    .car-price{
        padding: 0 .36rem;
        border-top: .2rem solid #edf1f6;
        div{
            padding: .3rem 0;
            a{
                color: #000;
                .message{
                    margin-left: .3rem;
                }
            }
        }
    }
    .test-text{
        background: #f0f4fa;
        color: #787878;
        padding: .4rem .4rem .05rem .4rem;
    }
</style>
