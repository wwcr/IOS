<style scoped>
    .search {
        text-align: center;
    }

    .text {
        width: 90%;
        height: 0.7rem;
        border-radius: 20px;
        text-align: left;
        background: #fff url(../../assets/img/search.png) no-repeat 32%;
        background-size: 4%;
        color: #787878;
        font-size: 0.32rem;
        text-indent: 6%;
        padding-left: 30%;
    }

    .center {

    }

    .currer {
        height: 0.9rem;
        background: #fff;
        margin-top: 0.2rem;
        font-size: 0.3rem;
        color: #1e1e1e;
        line-height: 0.9rem;
        padding: 0 0.5rem;
    }

    .currer p {
        display: inline-block;

    }

    .currer a {
        float: right;
        display: inline-block;
    }

    .currer a img {
        width: 0.3rem;
        margin-left: 0.2rem;
    }

    h5 {
        color: rgb(180, 180, 180);
        font-weight: normal;
        font-size: 0.28rem;
        margin-top: 0.3rem;
        padding: 0 0.5rem;
    }

    .ul_list {
        margin-top: 0.3rem;
        padding: 0 0.5rem;
    }

    .ul_list li {
        font-size: 0.4rem;
        color: #1e1e1e;
        width: 2.6rem;
        height: 1rem;
        background: #fff;
        line-height: 1rem;
        text-align: center;
        display: inline-block;
      margin-right: 0.3rem;
      margin-left: 0.3rem;
    }

    .ul_list li img {
        width: 0.38rem;
        margin-right: 0.15rem;
    }

    .order {
        margin-top: 0.2rem;
        border-top: 1px solid #f1f1f1;
    }

    .order p {
        padding: 0 0.5rem;
        font-size: 0.42rem;
        color: #787878;
        height: 0.72rem;
        line-height: 0.62rem;
    }

    .order_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
    }

    .order_list li {
        height: 1.2rem;
        line-height: 1.2rem;
        font-size: 0.42rem;
        color: #1e1e1e;
        margin-left: 0.5rem;
        border-bottom: 1px solid #f1f1f1;
    }

    .order_list li:last-child {
        border-bottom: none;
    }
</style>
<!-- 当前城市  -->
<template>
    <div class="city">
        <div class="search">
            <input v-model="search" class="text" type="text" placeholder="城市／行政区／拼音"/>
        </div>
        <div id="map">
            <baidu-map
                    :style="{'height': '0px'}"
                    class="maps" center="center"
                    :zoom="zoom"
                    :inertial-dragging="true"
                    @ready="handler">
                <!--配置定位-->
                <bm-geolocation
                        anchor="BMAP_ANCHOR_TOP_RIGHT"
                        :showAddressBar="true"
                        :autoLocation="true"
                        @locationSuccess="locationSuccess"
                        @locationError="locationError">
                </bm-geolocation>
            </baidu-map>
        </div>
        <div class="center">
            <div v-if="!search">
                <div>
                    <div class="currer">
                        <p>当前：{{address}}</p>
                        <a>选择<img src="../../assets/img/option.png"></a>
                    </div>
                    <h5>定位／最近城市</h5>
                    <ul class="ul_list">
                        <li><img src="../../assets/img/city_img.png">{{savecity.name}}</li>
                    </ul>
                </div>
                <h5>热门城市</h5>
                <ul class="ul_list">
                    <li @click="getCityName(x)" v-for="x in list.hot">{{x.name}}</li>
                </ul>
            </div>
            <div class="order" v-for="(x,index) in list.list">
                <p>{{index}}</p>
                <ul class="order_list">
                    <li @click="getCityName(item)" v-for="item in x">{{item.name}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import {BmlLushu} from 'vue-baidu-map'
    export default {
        name: 'hello',
        data () {
            return {
                msg:'',
                list:{},
                zoom:10,
                mecenter:{},
                savecity:{},
                address:'定位中...',
                search:'',
            }
        },
        components: {
            BmlLushu
        },
        watch:{
          'search':function (a,b) {
              this.searchFun();
              if(a == '')
              {
                  this.CarBrand();
              }
          }  
        },
        methods: {
            handler ({BMap, map}) {
                this.zoom = 12;
            },
            searchFun:function () {
                let that = this;
                this.Http('City/search',{
                    keyword:that.search
                },function (res) {
                    that.list = res;
                })
            },
            locationSuccess:function (point, AddressComponent) {
                this.mecenter = point.point;
                let address = '';
                address += point.addressComponent.province;
                address += point.addressComponent.city;
                address += point.addressComponent.district;
                address += point.addressComponent.street;
                address += point.addressComponent.streetNumber;
                this.address = address;
            },
            locationError:function (StatusCode) {
                layer.msg('定位失败')
            },
            getCityName:function (item) {
                console.log(item);
                let citynames = {};
                let savecity = localStorage.getItem('chose_city_once');
                if(JSON.parse(savecity)){
                    citynames = Object.assign({name:item.name},citynames)
                }
                localStorage.setItem('chose_city_once',JSON.stringify(citynames));
                location.href = '#/order/releasepage?c='+item.name
            },
            CarBrand(){
                let that = this;
                this.Http('City/getlist',{},function (res) {
                    that.list = res;
                })
            },
            getSavecity:function () {
                let savecity = localStorage.getItem('chose_city_once');
                let citynames = JSON.parse(savecity);
                if(citynames){
                    this.savecity = citynames;
                }
            }
        },
        created: function () {
            this.CarBrand();
            units.title.set('城市选择');
            this.getSavecity();
            this.$store.state.header.left = function () {
                location.href = '#/order/releasepage';
            };
        }
    }
</script>
