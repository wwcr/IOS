<!--页面css样式-->
<style scoped lang='scss'>
    .start{
        padding:0.5rem 0;
    }
    .kanhu{
        width: 100%;
        padding-bottom: 0.5rem;
      position: relative;
    }
    .kanhu img{
        width: 100%;
        height: 4.35rem;
    }
    .kanhu p{
      position: absolute;
      font-size: 0.66rem;
      color: #1e1e1e;
      right: 1.5rem;
      top: 1.8rem;
      font-weight: bold;
    }
    .find-car-page{
        border-top: .01rem solid #f0f4fa;
        background: #fff;
        font-size: .55rem;
        padding: .4rem;
        box-sizing: border-box;
        margin-bottom: .1rem;
        img{
            width: .8rem;
        }
        span{
            font-weight: 600;
            margin-left: .4rem;
            position: relative;
            top: .08rem;
            color: #000;
        }
    }
</style>
<!--服务开启-->
<template>
    <div class="start"  style="padding-top:1.7rem;">
        <div class="find-car-page" @click="goto('server/content')">
            <a>
                <img src="../../../src/assets/img/caricon1.png" alt="">
                <span>寻车管理</span>
            </a>
        </div>
        <div class="find-car-page" @click="goto('find/index')">
            <a>
                <img src="../../../src/assets/img/caricon2.png" alt="">
                <span>回收管理</span>
            </a>
        </div>
        <!-- <div class="kanhu">
            <a @click="goto('server/content')">
              <img src="../../../src/assets/img/card.jpg">
              <p>寻车管理</p> -->
                <!--<img src=".././../assets/img/img_32.png">-->
            <!-- </a>
        </div>
        <div class="kanhu">
            <a @click="goto('find/index')">
              <img src="../../../src/assets/img/writer.png">
              <p>执行管理</p>
            </a>
        </div> -->

        <!--<div class="kanhu">-->
            <!--<a @click="goto('find/index')">-->
                <!--<img src=".././../assets/img/img_30.png">-->
            <!--</a>-->
        <!--</div>-->
        <!--<div class="kanhu">-->
            <!--<a @click="goto('implement/list')">-->
                <!--<img src=".././../assets/img/img_30.png">-->
            <!--</a>-->
        <!--</div>-->
        <navcate></navcate>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    export default {
        mounted:function () {
            units.title.set('业务管理');
        },
        methods: {
            goto:function (goto) {
                this.href(goto);
            }
        },
        components: {
            navcate
        },
        created () {
            // this.$store.state.header.left = function () {
            //     // alert(11111111111)
            //     location.href = '#/vehicletool';
            // };
            this.$store.state.header.leftShow = false
            cookie.set('curr',1);
        },
        beforeRouteEnter: function (to, from, next) {
            if(!units.isLogin()){
                layer.msg('请先登录',2,function () {
                    location.href = '#/login';
                })
            }
            next();
        }
    }
</script>
