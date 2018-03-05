<style scoped>
    .map {
        width: 100%;
    }
    .map a {
        width: 90%;
        display: block;
        position: fixed;
        left: 5%;
        bottom: 10%;
    }

    .map a img {
        width: 100%;
        height: 100%;
    }

    .map_foot {
        height: 1.5rem;
        position: fixed;
        bottom: 0;
        background: #fff;
        width: 100%;
    }

    .map_foot ul li {
        width: 49.5%;
        border-right: 1px dashed #f1f1f1;
        padding: 0 6%;
        float: left;
        margin-top: 0.2rem;
    }

    .map_foot ul li img {
        width: 0.6rem;
        float: left;
        margin-right: 0.3rem;
        margin-top: 0.28rem;
    }

    .map_foot ul li .map_img {
        margin-top: 0.36rem;
    }

    .map_foot ul li p {
        color: #1e1e1e;
        font-size: 0.24rem;
        height: 0.3rem;
        line-height: 0.3rem;
        padding-top: 0.2rem;
    }

    .map_foot ul li span {
        color: #1e1e1e;
        font-size: 0.3rem;
        height: 0.3rem;
        line-height: 0.3rem;
        margin-top: 0.5rem;
        display: block;
    }

    .map_foot ul li:last-child {
        border-right: none;
    }
    .bg{
        width: 100%;
        height: auto;
    }
    .maps {
        width: 100%;
        height: 900px;
    }
</style>
<template>
    <div>
        <div class="baidumap" style="margin-top:0.05rem">
            <baidu-map
                    :style="{'height':window.height -1 + 'px'}"
                    class="maps"
                    :center="center"
                    :zoom="zoom"
                    :inertial-dragging="true"
                    @ready="handler">
                <!--配置瓦片地图(交通流情况)-->
                <bm-traffic :predictDate="{weekday: 7, hour: 12}"></bm-traffic>
                <!--配置瓦片地图-->
                <bm-tile
                        :isTransparentPng="true"
                        tileUrlTemplate="//developer.baidu.com/map/jsdemo/demo/tiles/{Z}/tile{X}_{Y}.png">
                </bm-tile>
                <!--缩放-->
                <bm-navigation anchor="BMAP_ANCHOR_BOTTOM_LEFT" :enableGeolocation="true"></bm-navigation>
                <!--配置定位-->
                <bm-geolocation
                        anchor="BMAP_ANCHOR_BOTTOM_RIGHT"
                        :showAddressBar="true"
                        :autoLocation="true"
                        @locationSuccess="locationSuccess"
                        @locationError="locationError">
                </bm-geolocation>
                <!--车的位置-->
                <bm-marker :position="center"
                           :dragging="false"
                           animation="BMAP_ANIMATION_BOUNCE"
                           :icon="card"></bm-marker>
                <!--人的位置-->
                <bm-marker :position="mecenter"
                           :dragging="false"
                           animation="BMAP_ANIMATION_BOUNCE"
                           :icon="me"></bm-marker>
                <!--导航路线-->
                <div class="daohang" v-if="daohang.open">
                    <bm-driving
                            :start="daohang.start"
                            :end="daohang.end"
                            @searchcomplete="handleSearchComplete"
                            :panel="false"
                            :rotation="true"
                            :content="car_content"
                            :autoViewport="true"></bm-driving>
                    <bml-lushu
                            @stop="reset"
                            :path="path"
                            :icon="icon"
                            :play="play"
                            :rotation="true"></bml-lushu>
                </div>
            </baidu-map>
        </div>
        <div class="map">
            <a @click="startGo"><img src="../../../src/assets/img/map.png"></a>
            <!-- <div class="map_foot">
                <ul>
                    <li>
                        <img class="map_img" src="../../../src/assets/img/time.png">
                        <div>
                            <p>拍摄时间</p>
                            <span>{{info.car_addtime}}</span>
                        </div>
                    </li>
                    <li>
                        <img src="../../../src/assets/img/map_img1.png">
                        <p>拍摄时间</p>
                        <span>{{info.car_addtime}}</span>
                    </li>
                </ul>
            </div> -->
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import cookie from '../../tools/cookie'
    import {BmlLushu} from 'vue-baidu-map'
    export default {
        name: 'map',
        components: {
            BmlLushu
        },
        data () {
            return {
                info:{},
                center: {lng: 0, lat: 0},
                zoom: 13,
                card:{
                    url:units.getHost()+'/public/images/p_car.png',
                    size: {
                        width: 300,
                        height: 157
                    }
                },
                mecenter:{
                    lng: 117.404,
                    lat: 39.215
                },
                me:{
                    url:units.getHost()+'/public/images/p_me.png',
                        size: {
                        width: 300,
                            height: 157
                    }
                },
                play: true,
                path: [],
                icon: {
                    url: 'http://api.map.baidu.com/library/LuShu/1.2/examples/car.png',
                    size: {width: 52, height: 26},
                    opts: {
                        anchor: {width: 27, height:13}
                    }
                },
                car_content:'正在前往',
                daohang:{
                    start:'',
                    end:'',
                    open:false
                }
            }
        },
        methods: {
            //开始导航
            startGo:function () {
                let that = this;
                if(that.daohang.start == ''){
                    layer.msg('抱歉,暂未获取您的位置,无法导航,您可以手动点击右下角的定位图标获取您的位置');
                    return false;
                }
                if(that.daohang.end == ''){
                    layer.msg('抱歉,暂未获取您爱车的位置,无法导航');
                    return false;
                }
                this.daohang.open = !this.daohang.open;
                new Promise(function () {
                    that.play = true;
                })
            },
            //停止导航
            reset () {
                this.play = false
            },
            handleSearchComplete (res) {
                this.path = res.getPlan(0).getRoute(0).getPath()
            },
            locationSuccess:function (point, AddressComponent) {
                this.mecenter = point.point;
                let address = '';
                address += point.addressComponent.province;
                address += point.addressComponent.city;
                address += point.addressComponent.district;
                address += point.addressComponent.street;
                address += point.addressComponent.streetNumber;
                this.daohang.start = address;
            },
            locationError:function (StatusCode) {
                layer.msg('定位失败')
            },
            handler ({BMap, map}) {
                console.log(BMap, map);
                this.zoom = 12;
            },
            len:function (str) {
                return str.substring(0,10);
            },
            getInfo(){
                let that = this;
                this.Http('map/info',{
                    id:that.$route.query.id
                },function (res) {
                    that.info = res.info;
                    if(that.info.location){
                        that.daohang.end = that.info.car_location;
                        that.center = that.info.location.location;
                    }
                })
            }
        },
        created: function () {
            this.getInfo();
            this.$store.state.header.left = function () {
                location.href = '#/server/content?cur=2';
            };
        },
        beforeCreate:function () {
            units.title.set('查看车辆');
        }
    }
</script>