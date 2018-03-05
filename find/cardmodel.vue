<style scoped>
    .voiture p {
        color: #787878;
        font-size: 0.42rem;
        height: 1rem;
        line-height: 1rem;
        padding: 0 0.5rem;
    }

    .ul_voiture {
        background: #fff;
        padding-right: 0.5rem;
    }

    .ul_voiture li {
        height: 1.2rem;
        line-height: 1.2rem;
        font-size: 0.42rem;
        color: #1e1e1e;
        margin-left: 0.5rem;
        border-bottom: 1px solid #f1f1f1;
        padding-right: 5%;
    }
    .ul_voiture span{
      margin-left: 0.3rem;
    }

    .ul_voiture li.cur {
        background: url(../../assets/img/img_39.jpg) no-repeat right;
        background-size: 5%;
    }
</style>
<!--车辆型号-->
<template>
    <div class="voiture">
        <div v-for="(x,index) in list">
            <p>{{x.name}}</p>
            <ul class="ul_voiture">
                <!--<li class="cur"></li>-->
                <li v-for="item in x.list" @click="getCityName(item)">
                    <img width="30" v-lazy="item.logo||'http://pic1.jisuapi.cn/car/static/images/logo/300/33690.png'">
                    <span>{{item.name}}</span>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    export default {
        name: 'hello',
        data () {
            return {
                msg:'',
                list:{},
                parentid:1
            }
        },
        methods: {
            getCityName:function (item) {
                console.log(item);
                location.href = '#/findcar?m='+item.name
            },
            CarBrand(){
                let that = this;
                this.Http('Car/CarType',{
                    parentid:that.parentid
                },function (res) {
                    that.list = res;
                })
            }
        },
        created: function () {
            this.CarBrand();
            units.title.set('车辆品牌');
            this.parentid = this.$route.query.parentid;
            this.$store.state.header.leftShow = false;
        }
    }
</script>
