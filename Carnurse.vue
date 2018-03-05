<!--页面css样式-->
<style scoped>
    .resg{
        background: #f2f6f7;
        font-size: 0.4rem;
        line-height: 0.6rem;
        padding: 0.52rem 0.38rem;
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
        line-height: 1.49rem;
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
</style>
<template>
    <!--车辆看护-->
    <div class="carnurse">
        <div class="resg">
            请填写一下信息，进行车辆看护服务。每辆车看护按年收费，每年580！
        </div>
        <div class="in_list clearfix">
            <ul>
                <li>
                    <a>
                        <label>车辆品牌</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                            <input type="text" v-model="form.card_brand" class="text" placeholder="奔驰">
                        </span>
                    </a>
                </li>
                 <li>
                    <a>
                        <label>车辆型号</label>
                        <span class="arrow_right_2"></span>
                        <span class="message">
                            <input type="text" v-model="form.card_model" class="text" placeholder="单行输入">
                        </span>
                    </a>
                </li>
                 <li>
                    <a>
                        <label>车牌号码</label>
                        <span class="arrow_right_2"></span>
                        <span class="message">
                            <input type="text" v-model="form.card_number" class="text" placeholder="单行输入">
                        </span>
                    </a>
                </li>
                 <li>
                    <a>
                        <label>车辆颜色</label>
                        <span class="arrow_right_2"></span>
                        <span class="message">
                            <input type="text" v-model="form.card_color" class="text" placeholder="单行输入">
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div class="sub_btn">
            <a @click="postData">提交</a>
        </div>
    </div>
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    export default {
        data () {
            return {
                form:{
                    card_brand:'宝马',
                    card_model:'x5',
                    card_number:'甘A88888',
                    card_color:'红色'
                }
            }
        },
        methods: {
            postData(){
                let that = this;
                let tips = ['车辆品牌','车辆型号','车牌号码','车辆颜色'];
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
                });
                if(next) return false;
                this.$http.post(units.host('carnurse'),units.params(this.form)).then(function (res) {
                    if(res.data.code > 0){
                        layer.msg('提交成功',2,function () {
                            location.href = '/pay?type=1&order='+res.data.code;
                        })
                    }else{
                        layer.msg(res.data.info)
                    }
                });
            }
        },
        created: function () {
            //1 车辆看护,2 寻车服务
            cookie.set('serviceType',1);
            units.title.set('车辆看护')
        },
        beforeCreate:function () {
            units.isLogin(true);
        }
    }
</script>
