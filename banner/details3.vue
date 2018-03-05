<!--页面css样式-->
<style scoped>
    .findcar {
        padding: 0.4rem;
      background: #fff;
    }

    .findcar h3 {
        color: #1e1e1e;
        font-size: 0.7rem;
        font-weight: normal;
        font-weight: 700;
        padding-top:1.25rem; 
        text-align: center;
    }

    .new {
        margin-top: 0.3rem;
        display: flex;
    }

    .new .p1 {
        color: #ccc;
        font-size: 0.3rem;
        display: block;
        flex: 1;
    }

    .new .p2 {
        display: block;
        font-size: 0.2rem;
        color: #999;
        flex: 1;
        text-align: right;
    }

    .new .p2 span {
        color: #999;
        border: 1px solid #999;
        font-size: 0.28rem;
        border-radius: 3px;
        padding: 0.05rem 0.1rem;
    }

    .article {
        font-size: 0.4rem;
        color: #1e1e1e;
        line-height: 0.7rem;
        margin-top: 0.4rem;
        letter-spacing: 0.01rem;
        font-weight: 300;
    }
    .cont_div{
        font-size: .41rem;
        margin-top: .25rem;
    }
    .cont_div img {
        width: 100%;
        margin: 0.3rem 0;
    }
    .commit img{
        width: 100%;
    }
    p{
        text-indent: .9rem;
    }
</style>
<template>
    <!--行业新闻  -->
    <div>
        <div id="Findcar" class="findcar">
            <h3>无维智慧车融，科技规避风险</h3>
            <div class="cont_div">
                <p>车融企业坏账等风险问题长久存在，尤其是贷后难点重重，深耕于行业发展方向，无维借助于互联网大趋势，以科技为依托，打造一款互联网汽车金融产品，解决汽车金融行业贷后寻车难收车难等问题。</p>
                <img src="http://h5.wwcrpt.com/public/banner/banner2.png" alt="">
                <p>“易寻”是北京无维科技有限公司自主开发的APP产品，服务于企业委托方和车辆执行方。企业寻车服务是由易寻平台自行提供，收车服务是由注册到平台的收车机构提供，委托方只需要在线发布订单即可在足不出户的情况下找到或收回相应车辆。订单全程受平台保护，提供全天24小时客服服务，可登录易寻APP随时了解车辆动态。</p>

                <p>无维独家拥有用于车辆查找的硬件设备，安全性能好且查找效率高；无维打造全国性的车辆数据库，通过无维硬件设备扫描到的车辆信息将不断丰富更新系统数据，并逐步建立和完善业务系统和违约车辆执行系统。</p>

                <p>大数据时代的到来是汽车金融行业的发展契机，无维运用互联网产品整合传统汽车金融行业的上下游资源，更好的解决车融行业关于寻车难收车难的问题，无维通过科技手段降低行业风险，创建全国性的汽车金融数据库，推动汽车金融行业生态圈的建立。</p>
            </div>
        </div>
        <div class="commit" @click="commit" v-if="false">
            <img src="../../assets/img/commit.jpg">
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    export default {
        data () {
            return {
                article: [],
                aid: '',
                host:units.getHost()
            }
        },
        created: function () {
            units.title.set('无维易寻')
        }
    }
</script>
