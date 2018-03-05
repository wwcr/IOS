<template>
    <div class="province-city-page" v-if='province'>
        <!-- <div class="province-title">省份</div> -->
        <!-- <div class="wrapper" ref='wrapper'> -->
            <!-- <div class="content">
                <ul class="province-content">
                    <li
                        v-for='(val, index) in province'
                        :key='val.id'
                        @click='checkProFn(val.id, val.citys, index)'
                    >
                        <span>{{val.pro}}</span>
                        <label for=""></label>
                    </li>
                </ul>
            </div>
        </div> -->
        <mt-index-list>
            <mt-index-section
                v-for='(val,ind,a) in province'
                :key='a'
                :index='ind'>
                <mt-cell 
                    v-for='(value, index) in val'
                    :key='value.id'
                    :title="value.pro"
                    @click.native="checkProFn(value.id, value.citys, index, ind)"
                ></mt-cell>
            </mt-index-section>
        </mt-index-list>
        <City
            v-show='cityFlag'
            :cityData = 'cityData'
            :proId = 'proId'
            :zimu = 'zimu'
            @closeCity = 'closeCity'
        />
    </div>
</template>
<script>

import City from './city'
import Bscroll from 'better-scroll'
import units from '@/tools/units'
import Vue from 'vue'
import { IndexList, IndexSection  } from 'mint-ui';
Vue.component(IndexList.name, IndexList);
Vue.component(IndexSection.name, IndexSection);
export default {
    name: 'CityPage',
    data () {
        return {
            cityData: [],
            cityFlag: false,
            province: [],
            proId:0,
            zimu: '' //索引字母
        }
    },
    methods : {
        checkProFn (id, city, index, ind) {//选择省份
            // console.log(id, JSON.parse(city))
            this.cityFlag = true
            this.proId = index
            this.zimu = ind
            this.cityData = JSON.parse(city)
        },
        closeCity (city) {
            if(city) { 
                this.$emit('closePro', city)
            }
            this.cityFlag = false
        }
    }, 
    created () {
        //获取省份数据
        // this.$http.post('/api/getwz_city').then(function (res) {
        //     if(res.ok) {
        //         this.province = res.body;             
        //     }
        // }); 
        this.$http.post(units.host('getwz_city', 'api')).then( function (res) {
            if(res.ok) {
                this.province = res.body;  
            }
        })
        this.$store.state.header.right = false
        units.title.set('城市选择');
        this.province = this.$route.params.data
    },
    updated () {
        // this.$nextTick(() => {
        //     this.scroll = new Bscroll(this.$refs.wrapper, {
        //         scrollY: true,
        //         scrollbar: true,
        //         click: true
        //     })
        // })
    },
    components: {
        City
    }
}
</script>
<style scoped lang='scss'>
    .province-city-page{
        padding-top: 1.25rem;
        font-size: .5rem;
        position: fixed;
        top:0;
        left: 0;
        bottom: 0;
        right: 0;
        .province-title{
            padding:.2rem .4rem;
            background: #f0f4fa;
            font-size: .4rem;
        }
        .wrapper {
            width: 100%;
            background: #fff;
            overflow: hidden;
            position: absolute;
            top: 2.2rem;
            bottom: 0;
            .content {
                position: absolute;
                padding: 0 10px;
                top: 0;
                left: 0;
                right: 0;
            }
        }
        .province-content{
            background: #fff;
            li{
                border-bottom: .01rem solid #f0f0f0; 
                line-height: 1.2rem;
                padding: 0 .4rem;
                display: flex;
                justify-content: space-between;
                label{
                    display: block;
                    width: 0.5rem;
                    height: 1.2rem;
                    background: url(../../assets/img/img_14.png) no-repeat;
                    background-position: right center;
                    background-size: auto 30%;
                }
            }
        }
    }
</style>
