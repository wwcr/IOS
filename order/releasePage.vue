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
                        <span  @click="carBrand()">
                            <span class="arrow_right_only"></span>
                            <span class="message">
                                <input
                                    type="text"
                                    v-model="form.card_brand"
                                    class="text"
                                    readonly
                                    placeholder="请选择车辆品牌">
                            </span>
                        </span>
                    </a>
                </li>
                <!-- <li>
                    <a>
                        <label>车辆型号</label>
                        <span class="arrow_right" @click="modelFn"></span>
                        <span class="message">
                          <input type="text" v-model="form.card_model" readonly
                                 class="text" placeholder="请选择车辆型号">
                            <div class="aui-list-item-input" id="card_model">
                                <select multiple='multiple'>
                                    <option v-for="(x, ind) in 100" :value="'ZT'+x" :key="ind">ZT{{x}}</option>
                                </select>
                            </div>
                        </span>
                    </a>
                </li> -->
                <li>
                    <a>
                        <label>车辆号码</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input type="text" v-model="form.card_allnumber" class="text" placeholder="请输入车牌号码"
                                 style="margin-left: 1.61rem;">
                            <div class="aui-list-item-input"
                                 style="position:absolute;top:0;width:1.6rem;top: .05rem;;overflow:hidden">
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
                <li class="mileage">
                    <a>
                        <label>合同金额</label>
                        <span class="arrow_right_text">万元</span>
                        <span class="message" style="width: 62%;">
                            <input 
                                type="number" 
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
                        <span class="message" style="width: 62%;">
                            <input type="number" v-model="form.card_contract" class="text" placeholder="请输入回收截止天数" >
                        </span>
                    </a>
                </li>
                <!-- <liv-on:
                    <a>
                        <label>车辆颜色</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" style="position:relative">
                          <input @click="scroll('card_color')" type="text" v-model="form.card_color" class="text"
                                 placeholder="请输入车辆颜色">
                        </span>
                    </a>
                </li> -->

                <!-- <li>
                    <a>
                        <label>违约城市</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                          <input readonly @click="scroll('card_city')" type="text" v-model="form.card_city" class="text"
                                 placeholder="请选择违约城市">
                            <div class="aui-list-item-input" id="card_city">
                                <select multiple='multiple'>
                                    <option value="北京">北京</option>
                                    <option value="上海">上海</option>
                                    <option value="深圳">深圳</option>
                                </select>
                            </div>
                        </span>
                    </a>
                </li>

                <li>
                    <a>
                        <label>寻车期限</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                             <div class="aui-list-item-input" id="card_contract">
                                 <input readonly type="datetime" v-model="form.card_contract" class="text"
                                        placeholder="请选择寻车期限">
                             </div>
                        </span>
                    </a>
                </li> -->
            </ul>
        </div>
        <div class="in_list1">
            <div class="time-city">
                <!-- <div class="li"  id='card_time2'>
                    <span>上牌时间</span>
                    <input type='text' readonly v-model='form.card_time' style="font-size: .4456rem;"/>
                    <b><img src='../../assets/img/down-jt.jpg'></b>
                </div> -->
                <div class="li">
                    <span>所在位置</span>
                    <span @click="carCity()">
                        <input
                            type='text'
                            v-model='form.card_city'
                            class="city-input"
                            readonly/>
                        <b><img src='../../assets/img/down-jt.jpg'></b>
                    </span>
                </div>
                <div class="li" @click='cardGps' style="position:relative;" >
                    <span>G P S</span>
                    <input type='text' v-model='form.card_gps' readonly style="position:relative;top:.06rem;"/>
                    <b><img src='../../assets/img/down-jt.jpg'></b>
                    <ul name="" id="select" v-show='selectFlag'>
                        <li @click='sureFn(1)'>是</li>
                        <li @click='sureFn(0)'>否</li>
                    </ul>
                </div>
            </div>
            <!-- <div class="time-city">
                <div class="li" id='card_contract2'>
                    <span>执行期限</span>
                    <input type='text' v-model='form.card_contract' readonly/>
                    <b><img src='../../assets/img/down-jt.jpg'></b>
                </div>
                <div class="li" @click='cardGps' style="position:relative;">
                    <span>G P S</span>
                    <input type='text' v-model='form.card_gps' readonly/>
                    <b><img src='../../assets/img/down-jt.jpg'></b>
                    <ul name="" id="select" v-show='selectFlag'>
                        <li @click='sureFn(1)'>是</li>
                        <li @click='sureFn(0)'>否</li>
                    </ul>
                </div>
            </div>-->
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

            <div class="car-price">
                <div>
                    <a>
                        <label>车辆佣金</label>
                        <!-- <span class="arrow_right_text" style="color: red;">提示建议8000</span> -->
                        <span class="message" style="width: 59%;margin-left: .9rem;">
                            <input type="number" v-model="form.card_price" placeholder="请输入车辆佣金" class="text">
                        </span>
                    </a>
                </div>
            </div>
            <div class="test-text">
                <span v-if="form.suggest_money > 0.8">
                    本次建议价: <span>0.80</span>  <span> - {{form.suggest_money}}</span> 万元
                </span>
                <span v-if="form.suggest_money < 0.8 && form.suggest_money>0">
                    本次建议价: <span>0.80</span>万元
                </span>
                <span v-if="form.suggest_money ==0.00 && !form.card_money">
                    本次建议价: <span>0</span>万元
                </span>
            </div>
        </div>
        <!-- <div class="pledge">
            <div class='license-title'>绿本抵押图片</div>
            <div class="picture">
                <img :src="imgstr.first" v-if="imgstr.first" class="thumb">
                <div><input type="file" class="file" @change="upload(1)"></div>

            </div>
            <div class='license-title'>抵押借贷合同</div>
            <div class="borrow">
                <div>
                    <input type="file" class="bow_file" @change="upload(2)">
                </div>
                <img :src="imgstr.second" v-if="imgstr.second" class="thumb">
            </div>

        </div> -->

        <div class="pledge img-page">
            <div class='license-title'>机动车登记图片</div>
            <div class="license-ul1">
                <div class="li">
                    <div class="img-box" v-model='form.card_img1' @click='zoom(1)'><div class="img-mark" v-show='isShow == form.card_img1'></div><img :src="imgstr.first" v-if="imgstr.first"></div>
                    <div class="upload-btn"><input type="file" @change="upload(1)"></div>
                </div>
                <div class="li">
                    <div class="img-box" v-model='form.card_img2' @click='zoom(3)'><div class="img-mark" v-show='isShow == form.card_img2'></div><img :src="imgstr.first1" v-if="imgstr.first1"></div>
                    <div class="upload-btn"><input type="file" @change="upload(3)"></div>
                </div>
                <div class="li"></div>
            </div>
            <div class='license-title' style="margin-top: .4rem;">签约合同图片</div>
            <div class="license-ul1">
                <div class="li">
                    <div class="img-box" v-model='form.card_img3' @click='zoom(2)'><div class="img-mark" v-show='isShow == form.card_img3'></div><img :src="imgstr.second" v-if="imgstr.second"></div>
                    <div class="upload-btn"><input type="file" @change="upload(2)"></div>
                </div>
                <div class="li">
                    <div class="img-box" v-model='form.card_img4' @click='zoom(4)'><div class="img-mark" v-show='isShow == form.card_img4'></div><img :src="imgstr.third" v-if="imgstr.third"></div>
                    <div class="upload-btn"><input type="file" @change="upload(4)"></div>
                </div>
                <div class="li">
                    <div class="img-box" v-model='form.card_img5' @click='zoom(5)'><div class="img-mark" v-show='isShow == form.card_img5'></div><img :src="imgstr.four" v-if="imgstr.four"></div>
                    <div class="upload-btn"><input type="file" @change="upload(5)"></div>
                </div>
            </div>
        </div>

        <div class="sub_btn">
            <a @click="postData">
                <span>提&emsp;交</span>
            </a>
        </div>
        <!--弹窗-->
        <div class="fixed-ad-layer" style="display: block;" v-if="false">
            <div class="fixed-ad-con">
                <a class="ad-img fixed-ad-img" href="">
                    <img src="../../assets/img/img_loding.png">
                    <p class="p1">审核中...</p>
                    <p class="p2">您信息已提交，工作人员正在审核，我们将在12小时内确认信息并通知您。</p>
                </a>
                <div class="close-fixed-ad"></div>
            </div>
        </div>
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
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import lrz from '../../../static/lrz/lrz.bundle'
    import scroll from '../../../static/mobiscroll/js/mobiscroll.jquery.min'
    import listInfo from '@/components/frame/indexList'
    import Province from '@/components/VehicleEvaluation/children/City/province'
    import Vue from 'vue'
    import { Picker } from 'mint-ui';
    Vue.component(Picker.name, Picker);
    import GpsPicker from '@/components/frame/gpsPicker'

    export default {
        name: 'index',
        data() {
            return {
                infoFlag: false,//车牌信息
                proFlag: false,
                brandList: [], //车牌数据
                ProList: [], //省份数据
                ex_term: '',
                o:1,
                form: {
                    card_brand: '',//品牌
                    card_number: '京',//号码   
                    card_allnumber:'',                 
                    contract_money:'',//合同金额
                    card_contract: '',//回收期限
                    card_city: '',//城市
                    card_gps: '否',
                    card_price: '',//佣金
                    card_img1: '',
                    card_img2: '',
                    card_img3: '',
                    card_img4: '',
                    card_img5: '',
                    allcard_img1:'',
                    allcard_img2:'',
                    // card_mileage: '',//公里数
                    // card_cards:'', //车牌后面数字
                    // card_time: '',//上牌时间
                    // card_money: '',//购买价格
                    // month: '', //月份
                    // year: '',//年,
                    // brand_num: '',//车型标识，
                    // pro_num:'',//省份标识
                    // city_num:'',//城市标识,
                    // evaluation: 0,//估价
                },
                imgstr: {
                   first: require('../../assets/img/jd-car1.jpg'),
                    second: require('../../assets/img/jd-car2.jpg'),
                    first1: require('../../assets/img/jd-car2.jpg'),
                    third:'',
                    four:'',
                    // five:'',
                },
                selectFlag: false,
                isShow: '', //是否显示图片遮罩
                card: {
                    card_brand: 0
                },
                gps: {
                    platform: '',
                    user: '',
                    pwd: ''
                },
                gpsShow: false,//是否显示gps信息
                gpsFlag:false,//是否显示gps弹窗
                cardata:{},
                cards:'',
                infoData: [],
                infoFlag: false,
                time: '',
                zl: ''
            }
        },
        watch:{
            'form.card_allnumber':function () {
                if(this.form.card_allnumber) {
                    this.form.card_allnumber = this.form.card_allnumber.toUpperCase()
                }
            }
        },
        methods: {
            countMoney () {
                if (this.form.card_gps == '是') {
                    this.form.suggest_money = (this.form.contract_money) * 0.2
                } else {
                    this.form.suggest_money = (this.form.contract_money) * 0.3
                }
                 this.form.suggest_money =  this.form.suggest_money.toFixed(2)
                console.log(this.form.suggest_money)
            },
            carBrand () { //车辆品牌
                this.infoFlag = true
                this.getData()
            },
            getData () { //获取车辆品牌数据
                this.$http.post(units.host('brandtest','api')).then( function (res) {
                    if (res.ok) {
                        this.brandList = res.body
                    }
                })
            },
            cardGps () {//选择是否GPS
               this.selectFlag = !this.selectFlag
            },
            sureFn (val){//点击是否GPS
                if(val == 1){
                    this.form.card_gps = '是',
                    this.gpsShow = true;
                    this.form.suggest_money = (this.form.contract_money) * 0.2
                }else {
                    this.gpsShow = false;
                    this.form.card_gps = '否',
                    this.form.suggest_money = (this.form.contract_money) * 0.3
                }
                this.form.suggest_money =  this.form.suggest_money.toFixed(2)
            },
            postData() {
                var jaxFlag = false;
                let that = this;
                if(this.gpsShow) {
                    let tips = ['车辆品牌', '车辆号码', '车辆号码','合同金额','回收期限','所在位置', 'GPS','车辆佣金','机动车登记图片','机动车登记图片', '签约合同图片', '签约合同图片', '签约合同图片','机动车登记图片','签约合同图片'];
                    let from = this.form;
                    let num = -1;
                    let next = false;
                    $.each(from, function (k, value) {
                        num++;
                        if (!value) {
                            layer.msg('请检查' + tips[num]);
                            next = true;
                            return false;
                        }else {
                            console.log(value);
                        }
                    });
                    // gps为是  账号密码不能为空 : '',
                    if(this.gps.platform == '' || this.gps.user == '' || this.gps.pwd == ''){
                    	layer.msg('请检查GPS信息');
                    	return false;
                    }
                  
                    if (next) return false;
                } else {
                	// return;
                    let tips = ['车辆品牌', '车辆号码','车辆号码', '合同金额','回收期限','所在位置', 'GPS','车辆佣金','机动车登记图片','机动车登记图片', '签约合同图片', '签约合同图片', '签约合同图片','机动车登记图片','签约合同图片'];
                    let from = this.form;
                    let num = -1;
                    let next = false;
                    $.each(from, function (k, value) {
                        num++;
                        console.log(k,num,value);
                        if (!value) {
                            console.log(num);
                            layer.msg('请检查' + tips[num]);
                            next = true;
                            return false;
                        }else {
                            console.log(value);
                        }
                    });
                    if (next) return false;
                }
                if(!units.isVehicleNumber(this.form.card_allnumber)){//判断车牌格式是否匹配
                    layer.msg('请填写正确的车牌格式');
                    return false;
                } 
                // return false;
                this.$http.post(units.host('findcarnew'), units.params(this.form)).then(function (res) {
                    if (res.data.code > 0) {
                        layer.msg(res.data.info, 2, function () {
                            cookie.del('findCarForm');
                            cookie.del('cards');
                            // console.log(res)
                            if(res.body.msg > 0){
                                that.Http('order/terrace', {
                                    ex_term: that.form.card_contract,
                                    ex_money: that.form.card_price,
                                    ex_fid: res.body.msg,
                                    ex_overdue: 1,
                                    ex_virecord: '是',
                                    ex_gps: that.form.card_gps,
                                    ex_location: that.form.card_city,
                                    ex_brand:that.form.card_brand,
                                    gps_platform: that.gps.platform,
                                    gps_user: that.gps.user,
                                    gps_pwd: that.gps.pwd

                                }, function (res) {
                                    layer.loading(false);
                                    console.log(res)
                                    if( cookie.get('sign_uesr') == 1){
                                        layer.msg('发布成功')
                                        return false;
                                    }
                                    if (res.code > 0) {
                                        that.href('order/pay?type=2&order=' + res.info+'&price='+that.form.card_price)
                                    } else {
                                        layer.msg(res.msg)
                                    }
                                })
                            }    // location.href = '#/server/terrace?id='+res.data.msg
                            // }else{
                            //     that.href('order/pay?type=2&order=' + res.data.code+'&price='+that.form.card_price)
                            // }
                        })
                    }
                });
            },
            // upload: function (id) {
            //     let self = this;
            //     if (event.target.files.length <= 0) {
            //         layer.msg('您未选中图片');
            //         return false;
            //     }
            //     layer.loading('上传中...');
            //     let reader = new FileReader();
            //     reader.readAsDataURL(event.target.files[0]);
            //     reader.onload = function (e) {
            //         let imgs = this.result;
            //         if (id == 1) self.imgstr.first = imgs;
            //         if (id == 2) self.imgstr.second = imgs;
            //         self.Http('units/imgstr', {
            //             imgstr: imgs
            //         }, function (res) {
            //             layer.loading(false);
            //             if (id == 1) self.form.card_img1 = res.info;
            //             if (id == 2) self.form.card_img2 = res.info;
            //         })
            //     };
            // },
            //
            upload: function (id) {
                let self = this;
                // alert(id);
                if (event.target.files.length <= 0) {
                    layer.msg('您未选中图片');
                    return false;
                }
                if(event.target.files[0].size/1024 >3000){
                    layer.msg('请选择小于2M的图片');
                    return false;
                }
                layer.loading('上传中...');
                let reader = new FileReader();
                reader.readAsDataURL(event.target.files[0]);
                reader.onload = function (e) {
                    let imgs = this.result;
                    switch(id){
                    	case 1:
	                    	self.imgstr.first = imgs;
	                    	self.form.card_img1 = 'img1';
	                    	break;
                    	case 2:
	                    	self.imgstr.second = imgs;
	                    	self.form.card_img3 = 'img2';
	                    	break;
                    	case 3:
	                    	self.imgstr.first1 = imgs;
	                    	self.form.card_img2 = 'img3';
	                    	break;
	                    case 4:
	                    	self.imgstr.third = imgs;
                    		self.form.card_img4 = 'img4';
                    		break;
                    	case 5:
                    		self.imgstr.four = imgs;
                    		self.form.card_img5 = 'img5';
                    		break;
                    }
                    this.isShow = imgs
                    self.Http('units/imgstr', {
                        imgstr: imgs
                    }, function (res) {
                        layer.loading(false);
                        // if (id == 1 || id == 3) self.form.allcard_img1 = self.form.allcard_img1 + '^' + res.info;
                        // if (id == 2 || id == 4 || id == 5) self.form.allcard_img2 = self.form.allcard_img2 + '^' + res.info;
                        switch(id){
                            case 1:
                            self.img1 = res.info;
                            self.form.allcard_img1 = res.info;
                            break;
                            case 2:
                            self.img2 = res.info;
                            self.form.allcard_img2 = self.img2;
                            break;
                            case 3:
                            self.img3 = res.info;
                            self.form.allcard_img1 = self.img1 +'^'+self.img3;
                            break;
                            case 4:
                            self.img4 = res.info;
                            self.form.allcard_img2 = self.img2 +'^'+self.img4;
                            break;
                            case 5:
                            self.img5 = res.info;
                            self.form.allcard_img2 = self.img2 +'^'+self.img4 + '^' + self.img5;
                            break;
                        }
                    })
                };


            },
            zoom (id) {
                var zoom ='',
                    that = this;
                if (id == 1) zoom = this.imgstr.first
                if (id == 2) zoom = this.imgstr.second;
                if (id == 3) zoom = this.imgstr.first1;
                if (id == 4) zoom = this.imgstr.third;
                if (id == 5) zoom = this.imgstr.four;
                    // console.log(zoom);
                layer.open({
                 type: 1,
                 content: '<img src="'+zoom+'" style="width:8rem";height:7rem;position:fixed; left:0;right:0;bottom:0;top:0;margin:auto;>',
                 anim: 'false',
                 style: 'border:none;',
                 success: function(elem){
                    that.forbidScroll()
                },
                end: function () {
                    that.startScroll()
                }
            });
            },
            cardtypes: function () {
                let that = this;
                setTimeout(function () {
                    //执行期限
                    $('#card_contract2').mobiscroll().date({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        max: new Date(2020, 7, 14),
                        min: new Date(2018, 7, 14),
                        onSet: function (event, inst) {
                            that.form.card_contract = event.valueText.replace(/\//g, "-");
                            that.ex_term = new Date(event.valueText)*1/1000
                        }
                    });//上牌时间
                    $('#card_time2').mobiscroll().date({
                        mode: 'scroller',
                        theme: 'mobiscroll',
                        lang: 'zh',
                        display: 'bottom',
                        max: new Date(new Date().getFullYear(), new Date().getMonth(), new Date().getDate()),
                        onSet: function (event, inst) {
                            that.form.card_time = event.valueText.replace(/\//g, "-");
                            that.form.year = event.valueText.split('/')[0]
                            that.form.month = event.valueText.split('/')[1]
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
                    location.href = '#/order/city'
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

            },
            modelFn () {
                this.infoFlag = true
            },
            carCity () {//获取城市数据
                this.$http.post(units.host('provincetest', 'api')).then( function (res) {
                    if (res.ok) {
                        this.ProList = res.body
                        this.proFlag = true
                        // console.log(res)
                    }
                })
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
            forbidScroll () {
                document.getElementsByTagName("html")[0].style.overflow="hidden";
                document.getElementsByTagName("html")[0].style.height="100%";
                document.getElementsByTagName("body")[0].style.overflow="hidden";
                document.getElementsByTagName("body")[0].style.height="100%"
            },
            startScroll () {
                document.getElementsByTagName("html")[0].style.overflow="visible";
                document.getElementsByTagName("html")[0].style.height="auto";
                document.getElementsByTagName("body")[0].style.overflow="visible";
                document.getElementsByTagName("body")[0].style.height="auto";
            },
        },
        beforeRouteLeave (to, from, next) {
            // console.log(this.$refs.detailInfo)
            if( this.infoFlag || this.proFlag) {//关闭品牌弹窗
                this.infoFlag = false
                this.proFlag = false
                next(from.path)
            } else {
                next()
            }
        },
        created: function () {
            //1 车辆看护,2 寻车服务
            this.getParm();
            cookie.set('serviceType', 2);
            units.title.set('发布订单');
            this.cardtypes();
            this.getCar();
            if(this.$route.query.zl)
            {
                this.zl = this.$route.query.zl;
            }
            this.$store.state.header.left = function () {
                location.href = '#/order/list';
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
            Province
        }
    }

</script>

<!--页面css样式-->
<style scoped lang='scss'>
    @import "../../../static/mobiscroll/css/mobiscroll.jquery.min.css";
    .gps-page{ //GPS信息margin
        border-top: .3rem solid #f1f1f1;
    }
    .license-ul1{
        display: flex;
        justify-content: space-between;
        .li{
            width: 3.1rem;
            .img-box{
                position: relative;
                width: 3.1rem;
                height: 3.1rem;
                background: url(../../assets/img/img_13.jpg);
                .img-mark{ //图片的遮罩
                    position: absolute;
                    top: 0;
                    left: 0;
                    right: 0;
                    bottom: 0;
                    background: rgba(0, 0, 0, .5);
                    width: 3.1rem;
                    height: 3.1rem;
                }
            }
            img{
                width: 3.1rem;
                height: 3.1rem;
            }
            .upload-btn{
                width: 3.1rem;
                height: 1rem;
                background: url(../../assets/img/upload-btn1.png) center;
                background-size:100%;
                input{
                    width: 100%;
                    opacity: 0;
                    font-size: .62rem;
                }
            }
        }
    }

    #select{
        position: absolute;
        width:5.3rem;
        top:1.3rem;
        left:0rem;
        background: #fff;
        border: .01rem solid #f0f4fa;
        z-index: 99;
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
        position: relative;
        top: -.05rem;
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
                .city-input{
                    top: .0rem;
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
        color: #fc5b5c;
        padding: .4rem .4rem .05rem .4rem;
        font-weight: 500;
    }

</style>