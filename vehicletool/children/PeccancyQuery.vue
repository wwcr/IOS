<template>
  <div class="peccancy-query">
        <p class="warn-info">请对照《机动车行驶证》认真填写以下内容</p>
        <ul class="peccanct-list">
            <li>
              <div>
                    <span class="check-title">车辆类型</span>
                    <span class="check-con">
                        <!-- <input type="checkbox" value="1" id="checkbox1" checked>
                        <label for="checkbox1"></label> -->
                        <b>小型车</b>
                    </span>
              </div>
            </li>
            <!-- <li>
                <a>
                    <label>查询城市</label>
                    <span class="arrow_right"></span>
                    <span class="message">
                        <input readonly @click="provinceFn('province')" type="text" v-model="form.card_city" class="text"
                                placeholder="请选择查询城市">
                    </span>
                </a>
            </li>
            <li>
                <a>
                    <label>车辆号码</label>
                    <span class="arrow_right_2"></span>
                    <span class="message" style="position:relative">
                        <input type="text" v-model="form.card_num" class="text" placeholder="请输入您的车牌号">
                    </span>
                </a>
            </li> -->
            <li>
              <div>
                    <span class="check-title">查询城市</span>
                    <span class="check-con">
                        <input 
                            readonly 
                            @click="provinceFn('province')" 
                            type="text" 
                            v-model="form.card_city" 
                            class="text"
                            style="font-size: .5rem;"
                            placeholder="请选择查询城市">
                    </span>
              </div>
            </li>
            <li>
              <div>
                    <span class="check-title">车辆号码</span>
                    <span class="check-con">
                        <input 
                            type="text" 
                            v-model="form.card_num" 
                            class="text" 
                            style="font-size: .5rem;"
                            placeholder="请输入您的车牌号">
                    </span>
              </div>
            </li>
            <li v-if='engineFlag'>
              <div>
                    <span class="check-title">发动机号</span>
                    <span class="check-con">
                        <input
                             type="text"
                             v-model="form.card_brand"
                             class="text"
                             style="font-size: .5rem;"
                             :placeholder=engineCon
                        />
                    </span>
              </div>
            </li>
            <li>
              <div>
                    <span class="check-title">车架号码</span>
                    <span class="check-con">
                        <input 
                            type="text" 
                            style="font-size: .5rem;"
                            v-model="form.card_model" 
                            :placeholder=modelCon
                            class="text" 
                            />
                    </span>
              </div>
            </li>
      </ul>
      <div class="query-btn-box"><button class="query-btn" @click='queryFn'>查&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;询</button></div>
  </div>
</template>
<script>
import units from '@/tools/units'
import cookie from '@/tools/cookie'
import ProvincePage from '@/components/ProvincePage'
export default {
    name: 'PeccancyQuery',
    data () {
        return {
                infoFlag: false,
                provinceFlag: false,
                engineFlag: 1,//是否需要发动机号
                engineno: 0, //输入全部还是后几位发动机
                engineCon: '请输入完整的发动机号',
                modelCon: '请输入完整的车架号',
                cardata:{},
                num: '-1',
                province: [],
                form: {
                    card_brand: '',//发动机号
                    card_model: '', //车架号
                    card_city: '',//城市名称
                    card_num:'' ,//车辆号码,、
                    card_code: ''//城市编号
                }
        }
    },
    methods: {
        modelFn () {
            this.infoFlag = true
        },//城市选择
        provinceFn ($name) {
            if($name === 'province' ) {
                localStorage.setItem('peccanctQuery', JSON.stringify(this.form));
                cookie.set('findCarForm', JSON.stringify(this.form));
                this.$router.push({name:'provincepage',params: {data: this.province}})
            }
        },
         queryFn() {//点击查询提交函数
            let tips = ['查询城市', '车牌号', '发动机号', '车架号'];
            let from = this.form;
            let next = false;
            $.each(from, function (k, value) {
                if (!value) {
                    layer.msg('请填写完整信息');
                    next = true;
                    return false;
                }
            });
            if (next) return false;
            this.$store.state.header.right = false

            ///参数
            let {
                card_code,
                card_num,
                card_brand,
                card_model
            } = this.form
            //请求违章数据
            this.$http.post(units.host('peccancy', 'api'),{
                    city:card_code,//城市
                    hphm:card_num,//车牌号
                    engineno: card_brand,//发动机号
                    classno:card_model,//车架号
                }).then( function (res) {
                    if(res.ok) {
                        console.log(res)
                        if (res.body.reason === '查询成功') {
                            let dataList = res.body.result
                            this.$router.push({path: 'peccancydetail', query: {dataList:dataList}})  
                        }else {
                            layer.msg('请填写正确的信息');
                        }        
                    }
            })
        },
    },
    created () {
        units.title.set('违章查询');
        this.$store.state.header.right = true;
        // this.getParm()
        this.form.card_city = this.$route.params.city
        let params = this.$route.params; //城市、id参数
        this.form.card_code = params.code

         
        this.$store.state.header.left = function () {
            // alert(11111111111)
            location.href = '#/vehicletool';
        };

        //获取省份数据
        this.$http.post(units.host('getwz_city', 'api')).then( function (res) {
            if(res.ok) {
                this.province = res.body;
                if (JSON.stringify(params) !== "{}") {
                    let cityInfo = JSON.parse(this.province[params.zimu][params.proId].citys)[params.cityInd]
                    // console.log(cityInfo)
                    this.engineFlag = cityInfo.engine*1  //是否需要发动机号码
                    this.engineno = cityInfo.engineno    //需要几位发动机号
                    if (cityInfo.classno*1) {
                        this.modelCon = '请输入车架号后'+cityInfo.classno+'位' //需要几位发动机号
                    }
                    

                    if (cityInfo.engineno*1) {
                        this.engineCon = '请输入发动机号后'+ cityInfo.engineno+'位'
                    }
                }              
            }
        })
    },
    components: {
        ProvincePage
    }
}
</script>

<style lang='scss' scoped>
    .peccancy-query{
        width:100%;
        padding-top:1.25rem;
        background: #f0f4fa;
        .warn-info{
            color: #ff3535;
            font-size: .3rem;
            padding: 0 .4rem;
            height: 1.1rem;
            line-height: 1.1rem; 
            background: #f0f4fa;
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
                 background: url('../../../assets/img/btn-bg.png') no-repeat;
                 background-size: cover;
             }
        }
        .peccanct-list{
            font-size: .47rem;
            background: #fff;
            li{
                // height: 1.5rem;
                // line-height: 1.5rem;
                padding:  .4rem 0;
                div{
                    // border-bottom:0.01rem solid #f0f0f0;
                }
            }
            .check-title{
                display: inline-block;
                width: 3rem;
            }
            .check-con{
                label{
                    margin-left:.25rem;
                }
            }
            
        }
    }
    .peccanct-list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }

    .peccanct-list li {
        // height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
        .check-title{
            font-size:.48rem;
        }
    }

    .peccanct-list li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        // height: 1.49rem;
        // line-height: 1.49rem;
        // min-height: 1.49rem;
    }

    .peccanct-list li a label {
        font-size: 0.48rem;
        color: #1e1e1e;
        display: inline-block;
        width: 3rem;
    }

    .peccanct-list .message {
        position: relative;
        float: right;
        margin: 0;
        // height: auto;
        width: 64%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        // line-height: 1.48rem;
        display: inline-block;
    }

    .peccanct-list .message input {
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
        width: 100%;
    }

    .peccanct-list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        // height: 1.48rem;
        background: url(../../../assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .peccanct-list li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.5rem;
        // height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }
    .aui-list-item-input{
        select{
            border: 0.01rem solid #297aff!important;
            height: .66rem;
            width: 1.3rem!important;
            color: #297aff!important;
            position: relative;
            top:0.1rem;
            font-size: 0.4rem;
            background: #fff;
        }
    }
    b{
        // margin-left:.3rem; 
        font-weight: normal;
    }
    .check-con {  
    // width: 25px;  
    // margin: 20px 100px;  
    position: relative;  
    left: -.05rem;
    }  
    .check-con input[type=checkbox] {  
        visibility: hidden;  
    }  
    .check-con label {  
        cursor: pointer;  
        position: absolute;  
        width: .55rem;  
        height: .55rem;  
        top: .08rem;  
        left: -0.3rem;  
        background: #fff;  
        border:2px solid #ccc;  
        -moz-border-radius: 3px;      /* Gecko browsers */  
        -webkit-border-radius: 3px;   /* Webkit browsers */  
        border-radius:3px;            /* W3C syntax */  
    }  
    .check-con label:after {  
        opacity: 0;  
        content: '\2714';  
        font-size: .2rem;
        text-align: center;
        position: absolute;  
        width: .45rem;  
        height: .43rem; 
        line-height: .43rem;
        border-radius:2px;      
        background: #2c7dfe;
        color: #fff;
        top: 0;  
        left: 0; 
    } 
    .check-con input[type=checkbox]:checked + label:after {  
        opacity: 1;
    }  
</style>
