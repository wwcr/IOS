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

    .cont_div img {
        width: 100%;
        margin: 0.3rem 0;
    }
    .commit img{
        width: 100%;
    }
</style>
<template>
    <!--行业新闻  -->
    <div>
        <div id="Findcar" class="findcar">
            <h3>{{article.art_title}}</h3>
            <div class="new">
                <p class="p1">{{article.art_time}}&nbsp;{{article.cate_name}}</p>
                <p class="p2">阅读&nbsp;{{Math.ceil(Math.random()*1000)}}</p>
            </div>
            <div class="cont_div">
                <p class="article" v-html="article.art_desc"></p>
                <img :src="host+article.art_thumb">
                <p class="article" v-html="article.art_content"></p>
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
        methods: {
            timeer: function (time) {
                return units.timemake(time)
            },
            more(){
                this.getArticle();
            },
            commit:function () {
                layer.msg('近期开放')
            },
            moreThatText: function () {
                return this.moreThat == true ? '查看更多' : '全部加载完成';
            },
            getArticle(){
                let that = this;
                this.$http.post(units.host('article'), {
                    swt: 'content',
                    id: this.aid
                }).then(function (res) {
                    this.article = res.data.info;
                });
            }
        },
        created: function () {
            this.aid = this.$route.query.id;
            this.getArticle();
            units.title.set('无维金融')
        }
    }
</script>
