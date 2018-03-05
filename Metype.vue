<!--页面css样式-->
<style scoped>
    .metype{
        background-size: 100% 100%;
        width: 100%;
        height: 100%;
        position: absolute;
    }
    .metype img{
        width: 100%;
        height: 100%;
    }
    .center{
        position: absolute;
        top: 15%;
        width: 90%;
        text-align: center;
        left: 5%;
    }
    .center img{
        width: 3rem;
        height: auto;
    }
    .center p{
        color: #ffc514;
        font-size: 1rem;
        text-align: center;
        padding: 0.5rem 0  0;
    }
    .center span{
        display: block;
        font-size: 0.38rem;
        color: #787878 ;
        padding:0.5rem;
        line-height: 0.7rem;
    }
    .center>div{
        padding: 0.5rem 0 0rem;
    }
    .center>div>dl{
        float: left;
        width: 33%;
        text-align: center;

    }
    .center>div>dl dt img{
    }
    .center>div>dl dd{
        color: #1e1e1e;
        font-size: 0.4rem;
    }
  .skip{
    position: absolute;
    bottom: -37%;
    right: 5px;
  }
  .skip a{
    color: red;
    font-size: 0.4rem;
  }
</style>
<template>
    <!--会员类型-->
    <div class="metype">
        <img src="../assets/img/img_20.png">
        <div class="center">
            <img src="../assets/img/img_3.png">
            <p>恭喜您!</p>
            <span>您已经成为无维金融服务平台的会员，下面您的身份，以便于我们推送更多的服务，谢谢</span>
            <div class="clearfix">
                <dl @click="chose(1)">
                    <dt><img src="../assets/img/img_22.png" style="width:0.96rem;height:1.26rem;"></dt>
                    <dd>委托方</dd>
                </dl>
                <dl @click="chose(2)">
                    <dt><img src="../assets/img/img_25.png" style="width:0.96rem;height:1.28rem;"></dt>
                    <dd>执行方</dd>
                </dl>
                <dl @click="chose(3)">
                    <dt><img src="../assets/img/img_23.png" style="width:1.68rem;height:1.22rem;"></dt>
                    <dd>以上两者</dd>
                </dl>
            </div>
          <div class="skip"><a href="#/login"><img style="width: 2rem" src="../assets/img/tiaoguo.png"></a></div>
        </div>

    </div>
</template>
<script>
    import units from '../tools/units'
    export default {
        name: 'index',
        data () {
            return {

            }
        },
        methods: {
            chose:function (id) {
                this.$http.post(units.host('Metype'),units.params({
                    id:id
                })).then(function (res) {
                    if(res.data.code > 0){
                        location.href = '#/Authentication';
                    }else{
                        layer.msg('选择失败,请重试');
                    }
                });
            }
        },
        created: function () {
            units.title.set('会员类型选择')
        }
    }
</script>
