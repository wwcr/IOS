<!--页面css样式-->
<style scoped>
    .img_div {
        width: 100%;
        text-align: center;
        margin: 1rem auto;
    }

    .img_div img {
        height: 1.66rem;
        width: 2.82rem;
    }

    .img_div p {
        color: #f6c31f;
        font-size: 1rem;
        text-align: center;
        padding: 0.5rem 0 0;
    }

    .img_div span {
        text-align: center;
        color: #828282;
        font-size: 0.38rem;
        display: block;
    }

    .btn {
        width: 100%;
        padding: 0.2rem 0.7rem 0;
    }

    .btn .btn_1 {
        background: #3d7fed;
        width: 42%;
        height: 1.4rem;
        line-height: 1.4rem;
        text-align: center;
        color: #fff;
        float: left;
        font-size: 0.45rem;
        border-radius: 5px;
    }

    .btn .btn_2 {
        background: #ffcb00;
        width: 42%;
        height: 1.4rem;
        line-height: 1.4rem;
        text-align: center;
        color: #fff;
        float: right;
        font-size: 0.45rem;
        border-radius: 5px;
    }

    .img {
        width: 100%;
        height: 100%;
        position: relative;
    }

    .daling {
        position: absolute;
        top: 15%;
    }

    .img_1 {
        width: 100%;
    }

    .ourder {
        position: absolute;
        bottom: 30%;
        width: 16%;
        height: 0.5rem;
        right: 27%;
    }

    .continue {
        position: absolute;
        bottom: 11.5%;
        width: 38%;
        height: 1rem;
        left: 8%;
    }

    .back {
        position: absolute;
        bottom: 11.5%;
        width: 38%;
        height: 1rem;
        right: 8%;
    }


</style>
<template>
    <div id="Findcar">
        <img class="img" src="../../src/assets/img/serve.jpg" :style="{'height':this.window.minHeight + 'px'}">
        <div class="daling">
            <img class="img_1" src="../../src/assets/img/save_1.png">
            <a class="ourder" @click="href('server/content?sid=2')"></a>
            <a class="continue" @click="href('findcar')"></a>
            <a class="back" @click="href('')"></a>
        </div>
        <!--<div class="img_div">-->
        <!--<img src="../assets/img/img_19.png">-->
        <!--<p>恭喜您!</p>-->
        <!--<span>已成功获得该车辆的看护</span>-->
        <!--</div>-->
        <!--<div class="btn">-->
        <!--&lt;!&ndash;<a v-if="$route.query.id == 2" href="/findcar" class="btn_1">继续添加</a>&ndash;&gt;-->
        <!--&lt;!&ndash;<a v-if="$route.query.id == 1" href="/carnurse" class="btn_1">继续添加</a>&ndash;&gt;-->
        <!--<a href="/" class="btn_2">返回</a>-->
        <!--</div>-->
    </div>
    <!--找车服务-->
</template>
<script type="text/javascript">
    export default {
        created: function () {
            this.units.title.set('服务开启');
            this.$store.state.header.leftShow = false;
        }
    }
</script>
