<!--页面css样式-->
<style rel="stylesheet/less" type="text/less" lang="less" scoped>
    body, html {
        background: #f4f4f4;
    }

    .w90 {
        width: 90%
    }

    .banner {
        width: 100%;
    }

    .banner img {
        width: 100%;
    }

    .center {
        width: 100%;
        background: #fff;
    }

    .center .seek {
        height: 2.48rem;
        border: 1px solid #f1f1f1;
        line-height: 2.48rem;
    }

    .center .seek img {
        width: 1.3rem;
        height: 1.3rem;
        float: left;
        margin-top: 0.6rem;
        margin-left: 3.5rem;
        margin-right: 0.4rem;
    }

    .center .seek p {
        font-size: 0.44rem;
        color: #1E1E1E;
    }

    .serve {
        height: 3.05rem;
        line-height: 3.05rem;
    }

    .serve ul li {
        width: 49.5%;
        border-right: 1px solid #f1f1f1;
        float: left;
    }

    .serve ul li img {
        width: 1.3rem;
        height: 1.3rem;
        float: left;
        margin: 0.8rem 0.4rem 0.8rem 0.8rem;
    }

    .serve ul li p {
        font-size: 0.44rem;
        color: #1E1E1E;
    }

    .serve ul li:last-child {
        border-right: none;
    }

    .lism {
        background: #fdfdfd;
        margin: 0 0.5rem 0 0.5rem;
        border-bottom: 1px solid #f1f1f1;
        padding: 0.5rem 0;
    }

    .img_left {
        float: left;
    }

    .img_left img {
        width: 0.7rem;
        height: 0.7rem;
    }

    .div_left {
        float: left;
        margin-left: 0.4rem;
        margin-top: 0.2rem;
    }

    .div_left p {
        font-size: 0.28rem;
        color: #828282;
    }

    .fiv_right {
        float: right;
        margin-right: 0.3rem;
    }

    .fiv_right img {
        width: 0.36rem;
    }

    .lism_cen {
        margin: 0.1rem 0 0.1rem;
    }

    .lism_cen dl dt {
        width: 23%;
        float: right;
    }

    .lism_cen dl dt img {

        width: 2.2rem;
        height: 1.5rem;
    }

    .lism_cen dl dd {
        width: 70%;
        font-size: 0.38rem;
        color: #282828;
        margin-bottom: 0.3rem;
    }

    .bianji {
        color: #999;
        font-size: 0.4rem;
        float: left;
    }

    .more {
        color: #999;
        font-size: 0.38rem;
        padding: 0.3rem;
        text-align: center;
        background: #f9f9f9;
    }

    .articleBox {
        margin-top: 0.3rem;
        background: #fff;
    }

    .message {
        width: 0.5rem;
        height: 0.5rem;
        float: right;
    }

    .lism_div {
        margin-top: 0.3rem;
    }
</style>
<template>
    <div id="index">
        <div class="banner">
            <swiper :options="swiperOption" ref="mySwiperA">
                <swiper-slide>
                    <img src="../../src/assets/img/banner.jpg">
                </swiper-slide>
                <swiper-slide>
                    <img src="../../src/assets/img/banner.jpg">
                </swiper-slide>
                <!-- Optional controls -->
                <div class="swiper-pagination"  slot="pagination"></div>
                <!--<div class="swiper-scrollbar"   slot="scrollbar"></div>-->
            </swiper>
        </div>
        <div class="center">
            <div class="seek" @click="hrefs('findcar')">
                <img src="../../src/assets/img/icon1.png">
                <p>寻车定位</p>
            </div>
            <div class="serve">
                <ul>
                    <li @click="hrefs('order/list')">
                        <img src="../../src/assets/img/icon2.png">
                        <p>回收车辆</p>
                    </li>
                    <li @click="hrefs('vehicletool')">
                        <img src="../../src/assets/img/icon3.png">
                        <p>车融助手</p>
                    </li>
                </ul>
            </div>
        </div>
        <div class="articleBox">
            <div class="cen_box" v-for="x in article">
                <div class="lism">
                    <!--<div class="lism_div clearfix">-->
                    <!--<div class="img_left"><img src="../assets/img/img_10.png"></div>-->
                    <!--<div class="div_left">-->
                    <!--<p>{{x.cate_name}}</p>-->
                    <!--<p>{{timeer(x.art_time)}}</p>-->
                    <!--</div>-->
                    <!--<div class="fiv_right"><img src="../assets/img/img_12.png"></div>-->
                    <!--</div>-->
                    <div class="lism_cen clearfix">
                        <a @click="href('article/content?id='+x.article_id)">
                            <dl>
                                <dt><img :src="host+x.art_thumb||'/static/img/img_13.28f6603.jpg'"></dt>
                                <dd>
                                    {{x.art_title}}
                                    <div class="lism_div">
                                        <p class="bianji">编辑：{{x.ad_name}}&nbsp;{{len(x.art_time)}}</p>
                                        <!--<img class="message" src="../../src/assets/img/icon4.png">-->
                                    </div>

                                </dd>
                            </dl>
                        </a>

                    </div>
                </div>
            </div>
            <i class="fa fa-bar-chart" aria-hidden="true"></i>
            <div class="more" @click="more">{{moreThatText()}}</div>
            <div class="fh"></div>
            <navcate></navcate>
        </div>
    </div>
    <!--首页-->
</template>
<script>
    import units from '../tools/units'
    import cookie from '../tools/cookie'
    import navcate from './template/navcate.vue'
    import { swiper, swiperSlide } from 'vue-awesome-swiper'
    export default {
        name: 'index',
        data () {
            return {
                article: [],
                articlePage: 1,
                articleLimit: 2,
                moreThat: true,
                host: units.getHost(),
                swiperOption: {
                    autoplay: 5000,
                    loop: true,
                    pagination: '.swiper-pagination',
                    onSlideChangeEnd: swiper => {}
                }
            }
        },
        computed: {
            swiper() {
                return this.$refs.mySwiperA.swiper
            }
        },
        components: {
            navcate,
            swiper,
            swiperSlide
        },
        methods: {
            hrefs:function ($url) {
                if(cookie.get('user_auth') == 0 ) {
                    layer.msg('请先进行资料认证')
                    return false;
                }
                if(units.isLogin(true)){
                    location.href = '#/'+$url;
                }
            },
            islogin(){},
            Goto: function (url, login) {
                if (login && !units.isLogin()) {
                    location.href = '/login'
                } else {
                    location.href = url;
                }
            },
            timeer: function (time) {
                return units.timemake(time)
            },
            len: function (a) {
                return a.substring(0, 10)
            },
            more(){
                this.getArticle();
            },
            moreThatText: function () {
                return this.moreThat == true ? '查看更多' : '全部加载完成';
            },
            getArticle(){
                let that = this;
                this.$http.post(units.host('indexArticle'), {
                    page: that.articlePage++,
                    limit: that.articleLimit
                }).then(function (res) {
                    let list = res.data.info.data;
                    if (list.length < that.articleLimit) {
                        that.moreThat = false;
                    }
                    for (let x in list) {
                        that.article.push(list[x]);
                    }
                });
            }
        },
        created: function () {
            let that = this;
            this.getArticle();
            units.title.set('无维金融');
        },
        mounted() {}
    }
</script>
