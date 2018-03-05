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
            <h3>一点“易寻”，让车辆易寻一点</h3>
            <div class="cont_div">
                <p>近年来，汽车金融行业呈现爆发式增长，井喷背后却隐忧渐显，不良贷款率持续走高，坏账问题接踵而至。车融企业不断调整策略，加强风控审核，也无法避免居高不下的坏账问题，骗贷、重复借贷等情况时有发生，这不仅增加了企业风险，同时也扰乱了整个汽车金融行业的发展秩序。</p>
                <img src="http://h5.wwcrpt.com/public/banner/banner1.png" alt="">
                <p>客户若发生坏账风险，企业在无法追回资金的情况下第一时间选择追回贷款车辆，而坏账客户并不会坐以待毙，即便贷款车辆装有GPS设备，也会被人工拆除或屏蔽设置，没有GPS轨迹导航的情况下人车失踪，企业很难追回车辆挽回损失，对企业来讲，车辆是最后的保护伞，所以发现问题车辆后企业将不遗余力找回车辆，寻车既是企业痛点也是难点所在，无维科技也是由此而生，全力解决企业寻车难的问题。</p>

                <p>无维拥有先进的车辆寻找设备，自主研发安全性高，后台轨迹实时查看，具有电子围栏等安全措施；车辆信息同步到企业大数据库，包括车辆位置、车辆轨迹等信息，不断丰富更新车辆系统云数据。</p>

                <p>“易寻”是无维科技自主研发的一款APP产品，企业方只需安装注册后在线发布订单即可，由易寻平台负责车辆查找，企业作为委托方可在线实时查看查找状态，并有7*24小时人工客服服务，随时解决客户问题，直至车辆查找成功。易寻平台本着为车融企业省时省力并争取最大效益为己任，全力改善汽车金融贷后新面貌。</p>
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
