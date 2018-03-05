<!--页面css样式-->
<style scoped>
    .resg{
        /*background: #f2f6f7;*/
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.38rem 0.3rem 0.3rem 0.3rem;
        float:left;
    }
    .titleClass{
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.38rem 0.3rem 0.3rem 0.3rem;
    }
    .cation {
        padding-top: 1.25rem;
    }
    .cation h5{
        color: #1e1e1e;
        width: 100%;
        text-align: center;
        font-size: 0.48rem;
        padding-top: 0.4rem;
    }
    .member h6{
        font-size: 0.5rem;
        padding: 0.38rem;
    }
    .in_list{
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }
    .in_list li{
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden ;
        margin-left: 0.4rem;
    }
    .in_list li a{
        display: block;
        position: relative;
        padding-right: 0.47rem;
        height: 1.49rem;
        line-height: 1.3rem;
        min-height: 1.49rem;
    }
    .in_list li a label{
        font-size: 0.48rem;
        color: #1e1e1e;
    }
    .in_list .message{
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 70%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.4rem;
        line-height: 1.44rem;
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
        background: url(../assets/img/img_14.png)no-repeat;
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
    .foot{
        color: #828282;
        font-size: 0.38rem;
        padding: 0 0.4rem 0.7rem;
    }
    .nav{
        width: 50%;
        height: 1rem;
        border:1px solid #377bee;
        border-radius: 5px;
        margin: 0.5rem auto;
    }
    .nav ul{
        width: 100%;
    }
    .nav ul li{
        border-right: 1px solid #377bee;
        font-size: 0.4rem;
        color: #377bee;
        width: 50%;
        float: left;
        height: 0.97rem;
        line-height: 0.97rem;
        text-align: center;
    }
    .nav ul li:last-child{
        border-right:none;
    }
    .nav ul li.cur{
        background: #377bee;
        color: #fff;
    }
    .denity{
        width: 100%;
        position: relative;
        background: white;
    }
    .denity ul li{
        width: 44%;
        height:200px;
        padding: 0.4rem;
        background: #f4f7fc;
        margin-bottom: 10px;
    }
    .denity ul li img{
        width: 70%;
        height:120px;
        margin-left:16%;
        margin-top: 16%;
    }
    .denity ul .personal_up{
        float: left;
        margin-left: 3%;
    }
    .denity ul .personal_down{
        float: right;
        margin-right: 3%;
        margin-left:right;
    }
    .denity ul .cardUpPosition{
        float: left;
        margin-left: 3%;
    }
    .denity ul .cardDownPosition{
        float: left;
        margin-left: 3%;
    }
    .denity ul li:last-child{
        float: right;
    }
    .sub_btn2{
        padding:0.63rem 0.4rem 1.3rem;
    }
    .denity ul li input{
        width: 100%;
        height: 3.63rem;
        position: absolute;
        top: 1.7rem;
        opacity: 0;
    }
    .denity ul li .file_up{
        left:1.2rem;
    }
    .denity ul li .file_down{
        left:6.5rem;
    }
    .denity ul li .legal_file_up{
        top: 3.1rem;
        left: 1rem;
    }
    .denity ul li input{
        width: 39%;
    }
    .denity ul li .legal_file_down{
        top: 3.1rem;
        left: 6rem;
    }
    .denity ul li .duty_file_up{
        top: 9.8rem;
        left: 1rem;
    }
    .denity ul li .duty_file_down{
        top: 10rem;
        left: 6rem;
    }
    .denity ul .personalWithCard .license_file{
        top: 16.5rem;
    }
    .denity ul .personalWithCard{
        width:90%;
        background: white;
        margin-right:5%;
        border: 1px solid #f4f7fc;
    }
    .denity ul .personalWithCard input{
        top: 8.5rem;
        left: 4rem;
    }
    .denity ul .personalWithCard img{
        width: 45%;
        margin-left: 30%;
        margin-top: 20px;
    }
</style>
<template>
    <!--会员认证-->
    <div class="cation">
        <h5 v-if="user.per_name.length<=0 && form.en_name.length<=0">填写认证信息</h5>
        <div class="nav" v-show="user.per_name.length<=0 && form.en_name.length<=0">
            <ul>
                <li :class="{'cur':current}" @click="change()">个人认证</li>
                <li :class="{'cur':!current}" @click="change()">企业认证</li>
            </ul>
        </div>
        <!-- 企业 -->
        <div class="enterprise" v-if="!current">
            <div class="member">
                <h6>企业资料</h6>
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>企业名称</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.en_name" v-model="form.en_name" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.en_name" type="text" class="text" placeholder="" >
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>注册资金</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.en_regmoney" v-model="form.en_regmoney" type="text" class="text" placeholder="" disabled>
                                    <input v-else="form.en_regmoney" v-model="form.en_regmoney" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>法人姓名</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.en_person_name" v-model="form.en_person_name" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.en_person_name" type="text" class="text" placeholder="">

                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.en_person_idcard" v-model="form.en_person_idcard" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.en_person_idcard" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系方式</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.en_contact" v-model="form.en_contact" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.en_contact" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="member">
                <h6>负责人资料</h6>
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>负责人</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.enuser_name" v-model="form.enuser_name" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.enuser_name" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.enuser_idcard" v-model="form.enuser_idcard" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.enuser_idcard" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系方式</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="form.enuser_contact" v-model="form.enuser_contact" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="form.enuser_contact" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <!-- <li>
                            <a>
                                <label>工作地址</label>
                                <span class="arrow_right"></span>
                                <span class="message">
                                    <input v-model="form.enuser_address" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li> -->
                        <li class="sizePosition">
                            <a v-if="form.en_name">
                                <label>工作地址</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-model="form.enuser_address" type="text" class="text" placeholder="" disabled>
                                </span>
                            </a>
                            <a v-else>
                                <label >工作地点</label>
                                <el-cascader style="line-height:1.1rem;"
                                    :options="options2"
                                    @active-item-change="handleItemChange"
                                    :props="props"
                                    @change = "getSelectedCity"
                                >
                                </el-cascader>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>

            <!-- 上传图片资料 -->
            <div class="member">
                <h6>企业信息录入</h6>
                <div class="titleClass" >
                    请上传认证资料以便顺利通过审核，上传信息和照片仅供平台审核使用，请放心上传。
                </div>
                <div class="denity clearfix">
                    <ul>
                        <h6 class="titleClass" >
                            法人身份证
                        </h6>
                        <li class="cardUpPosition">
                            <img :src="host+form.legal_idcard_up" v-if="form.legal_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <input v-if="!form.en_name" type="file" @change="uplaodFile1" class="legal_file_up">
                        </li>
                        <li class="cardDownPosition">
                            <img :src="host+form.legal_idcard_down" v-if="form.legal_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <input v-if="!form.en_name" type="file" @change="uplaodFile2" class="legal_file_down">
                        </li>
                        <h6 class="titleClass" >
                            负责人身份证
                        </h6>
                        <li class="cardUpPosition">
                            <img :src="host+form.duty_idcard_up" v-if="form.duty_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <input v-if="!form.en_name" type="file" @change="uplaodFile3" class="duty_file_up">
                        </li>
                        <li class="cardDownPosition">
                            <img :src="host+form.duty_idcard_down" v-if="form.duty_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <input v-if="!form.en_name" type="file" @change="uplaodFile4" class="duty_file_down">
                        </li>
                        <h6 class="titleClass" >
                            营业执照
                        </h6>
                        <li class="personalWithCard">
                            <img :src="host+form.license_card" v-if="form.license_card">
                            <img src="../assets/img/license.png" v-else>
                            <input v-if="!form.en_name" type="file" @change="uplaodFile5" class="license_file">
                        </li>
                    </ul>
                </div>
            </div>

            <div class="sub_btn">
                <a v-if="!form.en_name" @click="postData">保存</a>
            </div>
            <div v-if="!form.en_name" class="foot">请上传认证所需要资料，以便顺利通过审核，上传信息及照片仅供平台审核使用，请放心上传</div>
        </div>
        <!-- 个人 -->
        <div class="personal" v-if="current">
            <div class="member">
                <div class="in_list">
                    <ul>
                        <li>
                            <a>
                                <label>姓名</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="user.per_name" v-model="user.per_name" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="user.per_name" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>身份证号</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="user.per_idcard" v-model="user.per_idcard" type="text" class="text" placeholder="请输入身份证号" disabled>
                                    <input v-else v-model="user.per_idcard" type="text" class="text" placeholder="请输入身份证号">
                                </span>
                            </a>
                        </li>
                        <li>
                            <a>
                                <label>联系电话</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="user.per_iphone" v-model="user.per_iphone" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="user.per_iphone" type="text" class="text" placeholder="">
                                </span>
                            </a>
                        </li>
                        <li class="sizePosition">
                            <a v-if="user.per_name">
                                <label>工作地址</label>
                                <span class="arrow_right_2"></span>
                                <span class="message">
                                    <input v-if="user.per_address" v-model="user.per_address" type="text" class="text" placeholder="" disabled>
                                    <input v-else v-model="user.per_address" type="text" class="text" placeholder="" >
                                </span>
                            </a>
                            <a v-else>
                                <label>工作地点</label>
                                <el-cascader style="line-height:1.1rem;"
                                    :options="options2"
                                    @active-item-change="handleItemChange"
                                    :props="props"
                                    @change = "getSelectedCity"
                                >
                                </el-cascader>
                            </a>

                        </li>
                    </ul>
                </div>
            </div>
            <div class="member">
                <h6>个人信息录入</h6>
                <div class="titleClass" >
                    请上传认证人身份证正反面照片。
                </div>
                <div class="denity clearfix">
                    <ul>
                        <li class="personal_up">
                            <img :src="host+user.per_idcard_up" v-if="user.per_idcard_up">
                            <img  src="../assets/img/card_up.png" v-else>
                            <input v-if="!user.per_name" type="file" @change="uplaodUp" class="file_up">
                        </li>
                        <li class="personal_down">
                            <img :src="host+user.per_idcard_down" v-if="user.per_idcard_down">
                            <img src="../assets/img/card_down.png" v-else>
                            <input v-if="!user.per_name" type="file" @change="uplaodDown" class="file_down">
                        </li>
                        <div class="resg" >
                            请上传您的半身手持身份证照。
                        </div>
                        <li class="personalWithCard">
                            <img :src="host+user.personal_with_card" v-if="user.personal_with_card">
                            <img src="../assets/img/self_card.png" v-else>
                            <input v-if="!user.per_name" type="file" @change="uplaodPersonalCard">
                        </li>
                    </ul>
                </div>
                <div class="sub_btn sub_btn2">
                    <a v-if="user.per_name" @click="upgradeCompany" style="background:red;">升级企业认证</a>

                    <a v-if="!user.per_name && !form.en_name" @click="userPostData">提交信息</a>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                form:{
                    en_name:'',
                    en_regmoney:'',
                    en_person_name:'',
                    en_person_idcard:'',
                    en_contact:'',
                    enuser_name:'',
                    enuser_idcard:'',
                    enuser_contact:'',
                    legal_idcard_up:'',
                    legal_idcard_down:'',
                    duty_idcard_up:'',
                    duty_idcard_down:'',
                    license_card:'',
                    enuser_address:'',
                    city_id : '',
                },
                user:{
                    per_name:'',
                    per_idcard:'',
                    per_iphone:'',
                    per_idcard_up:'',
                    per_idcard_down:'',
                    personal_with_card:'',
                    per_address:'',
                    city_id : '',
                },
                current:true,
                host:units.getHost(),
                provinces:{},
                provinceId:'',
                provinceName:'',
                cityDatas:{},

                //级联选择器组件 by jfeng
                options2: [],
                props: {
                    value: 'label',
                    children: 'cities'
                },
            }
        },
        methods: {
            handleItemChange(val) {
                setTimeout(_ => {
                    this.getProvinceId(val);
                }, 100);
            },
            getSelectedCity(value) {
                this.user.per_address = value[0] + ',' + value[1];
                this.form.enuser_address = value[0] + ',' + value[1];
                // this.user.city = value[1];
                this.getCityId(value[1]);
            },

            upgradeCompany:function () {
                this.current = false;
                location.href="#/Authentication?current='detail'"
            },

            change:function () {
              this.current = !this.current
            },
            uplaodUp:function (e) {
                this.upload(e,1)
            },
            uplaodDown:function (e) {
                this.upload(e,2)
            },
            uplaodPersonalCard:function (e) {
                this.upload(e,3)
            },

            //企业上传相关资料 by jfeng
            uplaodFile1:function (e) {
                this.upload(e,'legal_idcard_up')
            },
            uplaodFile2:function (e) {
                this.upload(e,'legal_idcard_down')
            },
            uplaodFile3:function (e) {
                this.upload(e,'duty_idcard_up')
            },
            uplaodFile4:function (e) {
                this.upload(e,'duty_idcard_down')
            },
            uplaodFile5:function (e) {
                this.upload(e,'license_card')
            },

            upload:function (e,type) {
                let that = this;
                let file = e.target.files[0];
                let reader = new FileReader();
                reader.readAsDataURL(file);
                reader.onload = function (res) {
                    that.uploadStaer(function(res){
                        if(type==1) {
                            that.user.per_idcard_up = res.data.info;
                        }else if(type==2){
                            that.user.per_idcard_down = res.data.info;
                        }else if(type==3){
                            that.user.personal_with_card = res.data.info;
                        }else if(type == 'legal_idcard_up') {
                            that.form.legal_idcard_up = res.data.info;
                        }else if(type == 'legal_idcard_down') {
                            that.form.legal_idcard_down = res.data.info;
                        }else if(type == 'duty_idcard_up') {
                            that.form.duty_idcard_up = res.data.info;
                        }else if(type == 'duty_idcard_down') {
                            that.form.duty_idcard_down = res.data.info;
                        }else if(type == 'license_card') {
                            that.form.license_card = res.data.info;
                        }

                    },res.target.result);
                }
            },
            uploadStaer:function (fn,img) {
                let that = this;
                layer.loading('上传中...');
                that.$http.post(units.doname('index.php/index/Toolure/upload'),units.params({
                    imgStr:img
                })).then(function (res) {
                    layer.loading(false);
                    fn&&fn(res)
                });
            },
            validate:function (fn) {
                let that = this;
                let tips = ['企业名称','注册资金','法人姓名','法人身份证号','法人联系方式','负责人姓名','负责人身份证','负责人联系方式','法人身份证正面照','法人身份证反面照','负责人身份证正面照','负责人身份证反面照','营业执照','工作地点','城市'];
                let from = this.form;
                let num = -1;
                let next = false;
                $.each(from,function (k,value) {
                    num++;
                    if(!value) {
                        layer.msg('请检查'+tips[num]);
                        next = true;
                        return false;
                    }
                    if(k == 'en_person_name' || k == 'enuser_name'){
                        var patt = /[\u4e00-\u9fa5]/;
                        if(!patt.test(value)){
                            layer.msg(tips[num]+'只能输入中文,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'en_person_idcard' || k == 'enuser_idcard'){
                        // var pattern = /\d{15}|\d{17}[0-9Xx]/;
                        var pattern = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/
                        console.log(pattern.test(value));
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'en_contact' || k == 'enuser_contact'){
                        if(value.length != 11){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                });
                fn&&fn(next);
            },
            postData(){
                let that = this;
                this.validate(function (res) {
                    if(!res) {
                        layer.loading('请稍等...');
                        that.$http.post(units.host('Authentication?type=enterprise'),units.params(that.form)).then(function (res) {
                            layer.loading(false);
                            if(res.data.code > 0){
                                layer.msg('提交成功',2,function () {
                                    location.href = '#/';
                                })
                            }else{
                                layer.msg(res.data.info)
                            }
                        });
                    }
                })
            },
            userPostData:function () {
                let that = this;
                this.userPostValidate(function(next){
                    if(!next){
                        layer.loading('请稍等...');
                        that.$http.post(units.host('Authentication?type=user'),units.params(that.user)).then(function (res) {
                            layer.loading(false);
                            if(res.data.code > 0){
                                layer.msg('提交成功',2,function () {
                                    location.href = '#/';
                                })
                            }else{
                                layer.msg(res.data.info)
                            }
                        });
                    }
                })
            },
            userPostValidate:function (fn) {
                let tips = ['姓名','身份证号','联系电话','身份证正面','身份证反面','手持身份证','工作地点','城市id'];
                let from = this.user;
                let num = -1;
                let next = false;
                $.each(from,function (k,value) {
                    num++;
                    if(!value) {
                        layer.msg('请检查'+tips[num]);
                        next = true;
                        return false;
                    };
                    if(k == 'per_name')
                    {
                        var patt = /[\u4e00-\u9fa5]/;
                        if(!patt.test(value)){
                            layer.msg(tips[num]+'只能输入中文,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'per_iphone')
                    {
                        if(value.length != 11){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                    if(k == 'per_idcard')
                    {
                        // var pattern = /\d{15}|\d{17}[0-9Xx]/;
                        var pattern = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/
                        console.log(pattern.test(value),value);
                        if(!pattern.test(value)){
                            layer.msg(tips[num]+'输入有误,请检查');
                            next = true;
                            return false;
                        }
                    }
                });
                fn&&fn(next);
            },
            provinceList:function () {
                let  that = this;
                that.$http.post(units.host('provinceList', 'Admin'),{
                    switch:'province'
                }).then( function (res) {
                    that.provinces = res.data.info;
                    for (var province of that.provinces) {
                        this.options2.push({label: province.name, cities: [], key:province.id})
                    }
                })
            },

            getProvinceId:function (name) {
                let that = this;
                that.provinceName = name;
                that.$http.post(units.host('getProvinceId', 'Admin'),{
                    province:that.provinceName[0],
                }).then( function (res){
                    that.provinceId = res.data.info.id;
                    this.getCitys();
                })
            },

            getCityId:function (name) {
                let that = this;
                that.provinceName = name;
                that.$http.post(units.host('getProvinceId', 'Admin'),{
                    province:that.provinceName,
                }).then( function (res){
                    that.user.city_id = res.data.info.id;
                    that.form.city_id = res.data.info.id;
                })
            },

            getCitys:function () {
                let that = this;
                that.$http.post(units.host('cityList', 'Admin'),{
                    province_id : this.provinceId,
                }).then (function (res) {
                    this.cityDatas = res.data.info;
                    this.provinces.forEach(function(province,key){
                        if (province.id == that.provinceId) {
                            that.cityDatas.forEach(function (city,k) {
                                that.options2[key].cities.push({label:city.name});
                            })
                        }
                    })
                })
            },

            getUser : function () {
                let that = this;

                that.$http.post(units.host('user'),{
                    sw : 'info',
                    uid : cookie.get('user_id'),
                }).then( function (res){
                    if (res.data.info.user_anthen == 1) {
                        that.user = res.data.info.auth
                    }

                    if (res.data.info.user_anthen == 2) {
                        this.current = false;
                        that.form = res.data.info.auth
                    }
                })
            }

        },

        created () {
            units.title.set('会员认证');
            this.provinceList();
            this.getUser();
            console.log('asdasd',this.user);

        }
    }
</script>