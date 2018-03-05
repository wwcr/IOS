<style scoped>
    /*.voiture p {*/
        /*color: #787878;*/
        /*font-size: 0.32rem;*/
        /*height: 0.69rem;*/
        /*line-height: 0.69rem;*/
        /*padding: 0 0.5rem;*/
    /*}*/

    /*.ul_voiture {*/
        /*background: #fff;*/
        /*!*padding-right: 0.5rem;*!*/
    /*}*/

    /*.ul_voiture li {*/
        /*height: 1.2rem;*/
        /*line-height: 1.2rem;*/
        /*font-size: 0.32rem;*/
        /*color: #1e1e1e;*/
        /*margin-left: 0.5rem;*/
        /*border-bottom: 1px solid #f1f1f1;*/
        /*padding-right: 5%;*/
    /*}*/

    /*.ul_voiture li.cur {*/
        /*background: url(../../assets/img/img_39.jpg) no-repeat right;*/
        /*background-size: 5%;*/
    /*}*/
    .car h6{
      height:0.62rem;
      line-height: 0.62rem;
      font-size: 0.32rem;
      color: #787878;
      padding-left: 0.37rem;
    }
    .car ul{
      border-top: 1px solid #f1f1f1;
      background: #fff;
    }
    .car ul li {
      height: 1.19rem;

    }
    .car ul li span{
      float: left;
      width: 1.5rem;
      height: 1.19rem;
      vertical-align: middle;
      padding: 0 0.29rem;

    }
    .car ul li span img{
      width: 100%;
      vertical-align: middle;
    }
    .car ul li p{
      border-bottom: 1px solid #f1f1f1;
      margin-left:1.5rem;
      font-size: 0.42rem;
      color: #1e1e1e;
      height: 1.19rem;
      line-height: 1.19rem;
    }
    .car ul li:last-child{
      border-bottom:none;
    }
</style>
<!--车辆ppai-->
<template>
    <div class="voiture car">
        <div v-for="(x,index) in list">
            <h6>{{index}}</h6>
            <ul class="ul_voiture">
                <!--<li class="cur"></li>-->
                <li v-for="item in list[index]" @click="getCityName(item)">
                    <span><img width="30" v-lazy="item.logo||'http://pic1.jisuapi.cn/car/static/images/logo/300/33690.png'"></span>
                    <p>{{item.name}}</p>
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
                list:{}
            }
        },
        methods: {
            getCityName:function (item) {
                console.log(item);
                location.href = '#/findcar?b='+item.name + '&id='+item.id
            },
            CarBrand(){
                let that = this;
                this.Http('Car/CarBrand',{},function (res) {
                    that.list = res;
                })
            }
        },
        created: function () {
            this.CarBrand();
            units.title.set('车辆品牌');
            this.$store.state.header.leftShow = false;
        }
    }
</script>
