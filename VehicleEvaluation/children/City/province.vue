<template>
    <div class="province-city-page" v-if='ProList'>
        <!-- <div class="province-title">省份</div> -->
            <!-- <mt-index-list
                :show-indicator="false">
                    <template v-for='(val,index,a) in ProList'>
                        <mt-index-section
                        :key='index'
                        :index='index' 
                        >
                        <mt-cell 
                            v-for='(value) in val'
                            :title='value.proName' 
                            :key='value.proID'
                            @click.native="checkProFn(value)">
                        </mt-cell>
                    </mt-index-section>
                    </template>
            </mt-index-list> -->
            <mt-index-list>
                <mt-index-section
                    v-for='(val,index,a) in ProList'
                    :key='a'
                    :index='index'>
                    <mt-cell 
                        v-for='(value) in val'
                        :key='value.proID'
                        :title="value.proName"
                        @click.native="checkProFn(value)"
                    ></mt-cell>
                </mt-index-section>
            </mt-index-list>
        <City
            v-show='cityFlag'
            @closeCity='closeCity'
            :cityData='cityData'/>
    </div>
</template>
<script>
import units from '@/tools/units'
import Bscroll from 'better-scroll'
import City from './city'
import Vue from 'vue'
import { IndexList, IndexSection  } from 'mint-ui';
Vue.component(IndexList.name, IndexList);
Vue.component(IndexSection.name, IndexSection);
export default {
    name: 'CityPage',
    props: ['ProList'],
    data () {
        return {
            cityData: [],
            cityFlag: false,
            onlyPro: {}
        }
    },
    methods : {
        checkProFn (val) {//选择城市
            this.$http.post(units.host('city','api'),{id: val.proID}).then( function (res) {
                if (res.ok) {
                    this.cityData = res.body
                    this.onlyPro = val
                    this.cityFlag = true
                    // console.log(res)
                }
            })
        },
        closeCity (city) {//关闭城市
            if(city) {  
                this.$emit('closePro', {city: city, pro: this.onlyPro})
            }
            this.cityFlag = false
        }
    }, 
    created () {
        //获取省份数据
        // this.$store.state.header.right = false
        // units.title.set('城市选择');
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
    // .province-city-page{
    //     padding-top: 1.25rem;
    //     font-size: .5rem;
    //     position: fixed;
    //     top:0;
    //     left: 0;
    //     bottom: 0;
    //     right: 0;
        
    // }
    .province-city-page{
        /* position: fixed;
        top: 1.25rem; */
        background: #fff;
        width: 100%;
        position: fixed;
        top: 1.3rem;
        bottom: 0;
        font-size:.45rem;
        .province-title{
            padding:.2rem .4rem;
            background: #f0f4fa;
            font-size: .4rem;
        }
    }
//     a{
//         color: #000;
//     }
//    .mint-indexlist-nav {
//         position: absolute;
//         top: 0;
//         bottom: 0;
//         right: 0;
//         background-color: red;
//         border-left: 1px solid #ddd;
//         text-align: center;
//         -webkit-box-pack: center;
//         -ms-flex-pack: center;
//         justify-content: center;
//     }
//     .mint-cell{
//         border-bottom: .01rem solid #f0f0f0!important; 
//     }
</style>
