<template>
    <!--找车服务-->
    <div id="Findcar">
        <div class="resg">
            请如实填写需寻找车辆信息，本平台只提供寻车服务，该信息不做它用，请放心上传！
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <label>车辆品牌</label>
                        <span class="arrow_right_only"></span>
                        <span class="message">
                            <input 
                                type="text" 
                                readonly 
                                v-model="form.card_brand" 
                                class="text"
                                @click="carBrand('/api/brand')"
                                placeholder="请选择车辆品牌">
                        </span>
                    </a>
                </li>
                <!--<li>
                    <a>
                        <label>车辆型号</label>
                        <span class="arrow_right_only" @click="modelFn"></span>
                        <span class="message">
                          <input type="text" v-model="form.card_model"
                                 class="text" placeholder="请输入车辆型号">
                             <div class="aui-list-item-input" id="card_model">
                                <select multiple='multiple'>
                                    <option v-for="(x, ind) in 100" :value="'ZT'+x" :key="ind">ZT{{x}}</option>
                                </select>
                            </div> 
                        </span>
                    </a>
                </li>-->
                <li>
                    <a>
                        <label>车辆号码</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input type="text" v-model="cards" class="text" placeholder="请输入车牌号码"
                                 style="margin-left: 1.61rem;">
                            <div class="aui-list-item-input"
                                 style="position:absolute;top:.05rem;width:1.6rem;overflow:hidden">
                                <select autocomplete="off" v-model="form.card_number"
                                        style="border: none;width:1.5rem;color:#333">
                                    <option value="京" selected="selected">京</option>
                                    <option v-if="index>0" v-for="(x,index) in cardata"
                                            :value="x.j"
                                            :key='index'
                                            :index="index">{{x.j}}</option>
                                </select>
                            </div>
                        </span>
                    </a>
                </li>
                <!-- <li class="mileage">
                    <a>
                        <label>行驶里程</label>
                        <span class="arrow_right_text">万公里</span>
                        <span class="message" style="width: 60%;margin-left: .25rem;">
                            <input type="text" v-model="form.card_mileage" class="text">
                        </span>
                    </a>
                </li> -->
                <!-- <li>
                    <a>
                        <label>车辆颜色</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input @click="scroll('card_color')" type="text" v-model="form.card_color" class="text"
                                 placeholder="请输入车辆颜色">
                        </span>
                    </a>
                </li> -->

                <li>
                    <a>
                        <label>所在城市</label>
                        <span class="arrow_right_only"></span>
                        <span class="message">
                          <input readonly @click="scroll('card_city')" type="text" v-model="form.card_city" class="text"
                                 placeholder="请选择所在城市">
                            <!-- <div class="aui-list-item-input" id="card_city">
                                <select multiple='multiple'>
                                    <option value="北京">北京</option>
                                    <option value="上海">上海</option>
                                    <option value="深圳">深圳</option>
                                </select>
                            </div> -->
                        </span>
                    </a>
                </li>

                <li>
                    <a>
                        <label>寻车期限</label>
                        <span @click='card_contract'>
                            <span class="arrow_right_only"></span>
                            <span class="message">
                                <div class="aui-list-item-input" ><!--id="card_contract" -->
                                    <input readonly type="datetime" v-model="form.card_contract" class="text"
                                            placeholder="请选择寻车期限">
                                </div>
                            </span>
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>G&nbsp;&nbsp;&nbsp;P&nbsp;&nbsp;&nbsp;S</label>
                        <span @click='gpsFn'>
                            <span class="arrow_right_only"></span>
                            <span class="message">
                            <input readonly type="text" v-model="form.gps" class="text"
                                    placeholder="请选择是或无">
                            </span>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        
        <!-- 有GPS信息 -->
        <div class="gps-page">
            <ul class="in_list">
                <li>
                    <a>
                        <label>GPS平台</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input 
                            type="text" 
                            v-model="cards" 
                            class="text" 
                            style="width: 100%;"
                            placeholder="请输入所使用的GPS平台">
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>账&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;号</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input type="text" v-model="cards" class="text" placeholder="请输入GPS平台账号">
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>密&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;码</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input type="text" v-model="cards" class="text" placeholder="请输入GPS平台密码">
                        </span>
                    </a>
                </li>
            </ul>
        </div>

        <!-- <div class="pledge">
            <div class='license-title'>绿本抵押图片</div>
            <div class="picture">
                <img :src="imgstr.first" v-if="imgstr.first" class="thumb">
                <div><input type="file" class="file" @change="upload(1)"></div>
                <img :src="imgstr.first1" v-if="imgstr.first1" class="thumb1">
                <div><input type="file" class="file" @change="upload(3)"></div>
                
            </div>
            <div class='license-title'>抵押借贷合同</div>
            <div class="borrow">
                <div>
                    <input type="file" class="bow_file" @change="upload(2)">
                </div>
                <img :src="imgstr.second" v-if="imgstr.second" class="thumb">
            </div>
            <p class="aptitude">所需资料确定后添加  签署委托查找合同，并在提供<span class="pact" @click='contract'>电子合同</span>手动签字</p>
            
        </div> -->

        <div class="pledge img-page">
            <div class='license-title'>机动车登记图片</div>
            <div class="license-ul1">
                <div class="li">
                    <img src="../assets/img/img_13.jpg" alt="">
                    <div class="upload-btn"><input type="file"></div>
                </div>
                <div class="li">
                    <img src="../assets/img/img_13.jpg" alt="">
                    <div class="upload-btn"><input type="file"></div>
                </div>
                <div class="li"></div>
            </div>
            <div class='license-title' style="margin-top: .4rem;">签约合同</div>
            <div class="license-ul1">
                <div class="li">
                    <img src="../assets/img/img_13.jpg" alt="">
                    <div class="upload-btn"><input type="file"></div>
                </div>
                <div class="li">
                    <img src="../assets/img/img_13.jpg" alt="">
                    <div class="upload-btn"><input type="file"></div>
                </div>
                <div class="li">
                    <img src="../assets/img/img_13.jpg" alt="">
                    <div class="upload-btn"><input type="file"></div>
                </div>
            </div>
            <p class="aptitude">所需资料确定后添加  签署委托查找合同，并在提供<span class="pact" @click='contract'>电子合同</span>手动签字</p>
            
        </div>
        <div class="sub_btn">
            <a @click="postData">
                <!-- <span v-if="zl">下一步</span> -->
                <span>提&emsp;交</span>
            </a>
            <!-- <p class="pact" style="margin-top: .5rem;" @click='contract'>请点击委托回收协议签字。</p> -->
        </div>
        <!--弹窗-->
        <div class="fixed-ad-layer" style="display: block;" v-if="false">
            <div class="fixed-ad-con">
                <a class="ad-img fixed-ad-img" href="">
                    <img src="../../src/assets/img/img_loding.png">
                    <p class="p1">审核中...</p>
                    <p class="p2">您信息已提交，工作人员正在审核，我们将在12小时内确认信息并通知您。</p>
                </a>
                <div class="close-fixed-ad"></div>
            </div>
        </div>
        <!-- 车牌信息 -->
        <listInfo 
            :brandList='brandList'
            @closeBrand = 'closeBrand'
            ref='detailInfo'
            v-show = 'infoFlag'/>
        <!-- 寻车期限 -->
        <div class="card_contract-box" v-if='timeFlag'>
            <div class="btn-box">
                <button class="cancel-btn" @click="cancelTime">取消</button>
                <button class="sure-btn" @click="sureTime">确定</button>
            </div>
            <mt-picker :slots="slots" @change="onValuesChange"></mt-picker>
        </div>
        <!-- 是否GPS -->
        <GpsPicker
            v-if='gpsFlag'
            @closePicker= 'closePicker'
        />
    </div>
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    import lrz from '../../static/lrz/lrz.bundle'
    import listInfo from '@/components/frame/indexList'
    import scroll from '../../static/mobiscroll/js/mobiscroll.jquery.min'
    import Vue from 'vue'
    import { Picker } from 'mint-ui';
    Vue.component(Picker.name, Picker);
    import GpsPicker from '@/components/frame/gpsPicker'
    export default {
        name: 'index',
        data() {
            return {
                form: {
                    card_brand: '',
                    card_number: '京',
                    card_city: '',
                    card_contract: '',
                    card_img1: '',
                    card_img2: '',
                    car_ass_id: '',
                    gps: ''
                },
                imgstr: {
                    first: '',
                    second: '',
                    first1:'',
                    third:'',
                    four:'',
                    // five:'',
                },
                card: {
                    card_brand: 0
                },
                cardata:{},
                cards:'',
                zl:'',
                infoData: [],
                infoFlag: false,
                brandList: [],//车牌数据
                timeFlag: false, //寻车期限开关，
                gpsFlag: false, //gps开关
                slots: [ //寻车期限(mint-ui)
                    {
                        flex: 1,
                        values: ['', '6月', '12月', '18月', '24月', '30月', '36月', '42月', '48月'],
                        className: 'slot1',
                        textAlign: 'center'
                    }
                ]
            }
        },
        watch:{
            'cards':function () {
                if(this.cards) {
                    this.cards = this.cards.toUpperCase()
                }
            }
        },
        methods: {
            postData() {
                let that = this;
                let tips = ['车辆品牌', '车辆号码','违约城市','寻车期限','绿本抵押图片', '抵押借款合同'];
                let from = this.form;
                let num = -1;
                let next = false;
                console.log(from)
                $.each(from, function (k, value) {
                    num++;
                    if (!value) {
                        console.log(num);
                        layer.msg('请检查' + tips[num]);
                        next = true;
                        return false;
                    }
                });
                if (next) return false;
                this.form.card_number = this.form.card_number + this.cards;
                // console.log(this.form.card_number, this.cards)
                if (cookie.get('c_status')  == 0) {
                    layer.msg('请签署合同');
                    return false;
                }
                            console.log(that.form)
                this.$http.post(units.host('findcar'), units.params(this.form)).then(function (res) {
                    if (res.data.code > 0) {
                        layer.msg(res.data.info, 2, function () {
                            cookie.del('findCarForm');
                            cookie.del('cards');
                            if(that.zl == 'send'){
                                location.href = '#/server/terrace?id='+res.data.msg
                            }else{
                                that.href('pay?type=2&order=' + res.data.code)
                            }
                        })
                    }
                });
            },
            upload: function (id) {
                let self = this;
                // alert(id);
                if (event.target.files.length <= 0) {
                    layer.msg('您未选中图片');
                    return false;
                }
                layer.loading('上传中...');
                let reader = new FileReader();
                reader.readAsDataURL(event.target.files[0]);
                reader.onload = function (e) {
                    let imgs = this.result;
                    
                    if (id == 1) self.imgstr.first = imgs;
                    if (id == 2) self.imgstr.second = imgs;
                    if (id == 3) self.imgstr.first1 = imgs;
                    if (id == 4) self.imgstr.third = imgs;
                    if (id == 5) self.imgstr.four = imgs;
                    self.Http('units/imgstr', {
                        imgstr: imgs
                    }, function (res) {
                        layer.loading(false);
                        if (id == 1) self.form.card_img1 = res.info;
                        if (id == 3) self.form.card_img1 = self.form.card_img1+'^'+res.info;
                        console.log(self.form.card_img1);
                        // if (id == 3) self.form.card_img3 = res.info;
                        // if (id == 2) self.form.card_img2 = res.info;
                    })
                };
            },
            cardtypes: function () {
                let that = this;
                setTimeout(function () {
                    $('#cards').mobiscroll().select({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        minWidth: 200,
                        placeholder: '请选择车辆品牌',
                        onSet: function (event, inst) {
                            that.form.card_brand = inst['_tempWheelArray'][0];
                        }
                    });
                    $('#card_model').mobiscroll().select({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        minWidth: 200,
                        placeholder: '请选择车辆型号',
                        onSet: function (event, inst) {
                            that.form.card_model = inst['_tempWheelArray'][0];
                        }
                    });
                    $('#card_color').mobiscroll().select({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        minWidth: 200,
                        placeholder: '请选择车辆颜色',
                        onSet: function (event, inst) {
                            that.form.card_color = inst['_tempWheelArray'][0];
                        }
                    });
                    $('#card_contract').mobiscroll().date({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        // max: new Date(new Date().getFullYear(), new Date().getMonth(), new Date().getDate()),
                        max: new Date(2020, 7, 14),
                        min: new Date(2018, 7, 14),
                        onSet: function (event, inst) {
                            that.form.card_contract = event.valueText.replace(/\//g, "-");
                        }
                    });
                    $('#card_city').mobiscroll().select({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        minWidth: 200,
                        placeholder: '请选择违约城市',
                        onSet: function (event, inst) {
                            that.form.card_city = inst['_tempWheelArray'][0];
                        }
                    });
                }, 20)
            },
            scroll: function ($name) {
                cookie.set('findCarForm', JSON.stringify(this.form));
                cookie.set('cards', this.cards);
                cookie.set('zl', this.zl);
                if ($name == 'cards') {
                    location.href = '#/find/voiture'
                }
                if ($name == 'card_model') {
                    location.href = '#/find/cardmodel?parentid=' + cookie.get('card_brand_id')
                }
                if ($name == 'card_city') {
                    location.href = '#/find/city'
                }
                //$('#'+$name).mobiscroll('show');
            },
            getParm: function () {
                let cookdata = cookie.get('findCarForm');
                this.cards = cookie.get('cards') != null ? cookie.get('cards'):'';
                this.zl = cookie.get('zl') != null ? cookie.get('zl'):''
                if (cookdata) this.form = JSON.parse(cookdata);
                new Promise(() => {
                    let par = this.$route.query;
                    if (par.c) this.form.card_city = par.c;
                    if (par.m) this.form.card_model = par.m;
                    if (par.b) {
                        this.form.card_brand = par.b;
                        this.card.card_brand = par.id;
                        cookie.set('card_brand_id',par.id);
                        this.form.card_model = '';
                    }
                })
            },
            getCar:function () {
                let that = this;
                this.$http.post(units.host('car','Toolure'), units.params()).then(function (res) {
                    that.cardata = res.data;
                });
            },
            brand () { //车辆品牌
                // this.$store.state.title = '车辆品牌';
                this.infoFlag = true
                // console.log(this.$store.state)
                // this.$http.post('/api/province').then(function (res) {
                //     console.log(res);
                // });
            },
            modelFn () {
                this.infoFlag = true
            },
            contract () {//签署电子合
                if(cookie.get('c_status') == '1'){//判断是否已经签署合同
                    this.$router.push('contracted')
                }else {
                    this.$router.push('contract')
                }
            },
            carBrand (url) { //车辆品牌
                this.infoFlag = true
                this.getData(url)
            },
            getData (url) { //获取车辆品牌数据
                // this.$http.post(url).then(function (res) {
                //     if (res.ok) {
                //         this.brandList = res.body
                //     }
                // });
                this.$http.post(units.host('brandtest', 'api')).then( function (res) {
                     if (res.ok) {
                        this.brandList = res.body
                        // console.log(res,1111)
                    }
                })
            },
            card_contract () {  //寻车期限
                this.timeFlag = true
            },
            onValuesChange(picker, values) {//寻车期限（mint-ui）
                // console.log(picker, values)
                this.form.card_contract = values[0]
                // if (values[0] > values[1]) {
                //     picker.setSlotValue(1, values[0]);
                // }
            },
            cancelTime () { //寻车期限滑块取消按钮
                this.form.card_contract = ''
                this.timeFlag = false
            },
            sureTime () { //寻车期限滑块确定按钮
                this.timeFlag = false
            },
            gpsFn () { //选择gps
                this.gpsFlag = true
            },
            closePicker (obj) {//关闭GPS
                if( obj.id == 0 ){
                    this.form.gps = ''
                }else{
                    this.form.gps = obj.gps
                }
                this.gpsFlag = false
            },
            closeBrand (val) { //关闭车辆品牌弹出框
                this.infoFlag = false
                this.form.card_brand = val.cxname
                this.form.car_ass_id = val.id
            },
            brand () { //车辆品牌
                // this.$store.state.title = '车辆品牌';
                this.infoFlag = true
                // console.log(this.$store.state)
                // this.$http.post('/api/province').then(function (res) {
                //     console.log(res);
                // });
            },
        },
        // beforeRouteLeave (to, from, next) {
        //     console.log(this.$refs.detailInfo)
        //     if( this.infoFlag ) {
        //         this.infoFlag = false
        //         this.$store.state.header.left = function () {
        //             location.href = '#/findcar';
        //         };
        //     } else {
        //         next()
        //     }
        // },
        created: function () {
            //1 车辆看护,2 寻车服务
            this.getParm();
            cookie.set('serviceType', 2);
            units.title.set('寻车定位');
            this.cardtypes();
            this.getCar();
            if(this.$route.query.zl)
            {
                this.zl = this.$route.query.zl;
            }
            this.$store.state.header.left = function () {
                location.href = '#/';
            };
            
        },
        mountd: function () {
        },
        beforeCreate: function () {
           console.log('beforeCreate')
        },
        beforeRouteEnter: function (to, from, next) {
            if(from.name == 'index' || from.name == 'orderList'){
                cookie.del('findCarForm');
                cookie.del('cards');
                cookie.del('zl');
                cookie.del('card_brand_id');
            }
            units.isLogin(true);
            next();
        },
        components: {
            listInfo,
            GpsPicker
        }
    }

</script>

<!--页面css样式-->
<style scoped lang='scss'>
    @import "../../static/mobiscroll/css/mobiscroll.jquery.min.css";
    // 机动车登记图片
    .license-ul1{
        display: flex;
        justify-content: space-between;
        .li{
            width: 3.1rem;
            img{
                width: 3.1rem;
                height: 3.1rem;
            }
            .upload-btn{
                width: 3.1rem;
                height: 1rem;
                background: url(../assets/img/upload-btn1.png) center;
                background-size:100%; 
                input{
                    width: 90%;
                    opacity: 0;
                }
            }
        }
    }
    // gps内容
    .gps-page{
        margin-top: .25rem;
    }
    // 寻车期限
    .card_contract-box{
        background: #fff;
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        padding: .5rem 0;
        .btn-box{
            display: flex;
            justify-content: space-between;
            button{
                width: 2rem;
                height: 1rem;
                font-size: .5rem;
                margin: 0 .5rem;
                border: 0;
                background:#fff;
            }
        }
    }
    .license-title{
        font-size: .48rem;
        padding-bottom:.4rem; 
    }
    #Findcar{
        padding-top:1.25rem; 
        background: #f0f0f0;
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
        position: relative;
        top: -.07rem;
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
        // font-family: "微软雅黑";
        // font-family: 'Droidsansfallback';
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
    }
    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background: url(../assets/img/img_14.png) no-repeat;
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

    .in_list li a .arrow_right_2 {
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
        background-size: 50%;
        overflow: hidden;
        display: flex;
        flex-wrap: wrap;
        padding-bottom:.3rem; 
        padding-right:.3rem; 
        img{
            width:2.1rem;
            height: 2.1rem;
            text-align: center;
            position: relative;
            top: .3rem;
            left: .3rem;        
        }
        .thumb1{
            margin-left:2rem;
            border:2px red solid;  
        }
        div{
            background: url(../../src/assets/img/license_bg.png) no-repeat center;
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
            background: url(../../src/assets/img/license_bg.png) no-repeat center;
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
        text-align: center;
        position: absolute;
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
        background: url(../../src/assets/img/xxxx.png);
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
   
</style>