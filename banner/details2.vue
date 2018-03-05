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
            <h3>易寻讲效率，收车无距离</h3>
            <div class="cont_div">
                <p>汽车金融企业近年来业务增长迅速，但贷前审批即使再严，也会出现一部分逾期客户通过常规电催，家访所无法解决，若想“短平快”的解决这批客户，在车融企业长期的业务实战中，外包执行公司是解决这类不良资产的一只主要力量。</p>
                <img src="http://h5.wwcrpt.com/public/banner/banner.png" alt="">
                <p>外包收车虽然省时省力，但也会有相应问题出现，如收取高额服务费、收车效率低、车辆受损，违约无保证等问题让企业方望而却步。在“易寻”平台就可以完全解决这些后顾之忧，“短平快”不再是口号，而是行动的象征。</p>

                <p>“易寻”拥有全国范围内的收车网点，覆盖全国大小城市，真正做到收车无距离；委托方设置收车期限，平台保证收车效率，随时查看收车状态，人工客服全天24小时服务直至车辆交接成功。</p>

                <p>“易寻”平台不断吸纳收车机构，系统审核通过后可在平台申请接单，由相应的区域经理分发执行任务，完成任务后获取相应佣金。易寻不断发展壮大收车机构，一方面服务于企业委托方，能够快速高效的完成收车业务， 另一方面也为执行方提供更大的客单量，作为连接委托方和需求方的服务平台，易寻全力实现双方利益最大化。</p>
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
