<template>
    <div class="city-city-page" v-if='cityData'>
        <div class="city-title">城市<span class="closeBtn" @click="checkCityFn(0)">×</span></div>
        <div class="wrapper" ref='wrapper'>
            <div class="content">
                <ul class="city-content">
                    <li
                        v-for='(val, index) in cityData'
                        :key='index'
                        @click='checkCityFn(val)'
                    >
                        <span>{{val.cityName}}</span>
                        <label for=""></label>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>
<script>
import units from '@/tools/units'
import Bscroll from 'better-scroll'
export default {
    name: 'CityPage',
    props: ['cityData'],
    methods : {  
        checkCityFn (city) {
            this.$emit('closeCity', city)
        }
    },
    updated () {
        this.$nextTick(() => {
            this.scroll = new Bscroll(this.$refs.wrapper, {
                scrollY: true,
                scrollbar: true,
                click: true
            })
        })
    }
}
</script>
<style scoped lang='scss'>
    .city-city-page{
        padding-top: 1.25rem;
        font-size: .5rem;
        position: fixed;
        top:0;
        bottom: 0;
        right: 0;
        z-index: 99;
        width: 45%;
        border-left: .2rem solid #f0f4fa;
        .city-title{
            padding:.2rem .7rem;
            background: #f0f4fa;
            font-size: .4rem;
            position: relative;
            width: 100%;
            .closeBtn{
                position: absolute;
                top:.1rem;
                right: .5rem;
                font-size: .7rem;
            }
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
        .city-content{
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
                    background-position: right center;
                    background-size: auto 30%;
                }
            }
        }
    }
</style>
