<template>
    <div class="city-page-box">
        <div class="city-title">城市<span class="closeBtn" @click="closeModel(0)">×</span></div>
        <div class="wrapper" ref='wrapper'>
            <div class="content">
                <ul class="city-content">
                    <li
                        v-for='(val,ind) in cityData'
                        :key='ind'
                        @click='checkCityFn(val.city_name, ind,val.city_code)'
                    >
                        <span>{{val.city_name}}</span>
                        <label for=""></label>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>
<script>
import Bscroll from 'better-scroll'
export default {
    name:'city',
    props: ['cityData', 'proId', 'zimu'],
    methods: {
        checkCityFn (city, ind,code) {
            this.$router.push({name:'peccancquery', params: {city: city, cityInd: ind, proId: this.proId, code: code, zimu: this.zimu}})
            // this.$emit('closeCity',{city: city, ind: ind})
        },
        closeModel (val) {
            this.$emit('closeCity',val)
        }
    },
    created () {
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
    .city-page-box{
        padding-top: 1.25rem;
        border-left:.2rem solid  #f0f4fa;
        font-size: .5rem;
        width: 60%;
        position: fixed;
        background: #fff;
        right:0;
        top:0rem;
        bottom: 0;
        .city-title{
            padding:.2rem .4rem;
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
            // height: 100%;
            z-index: 99;
            .content {
                position: relative;
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
            }
        }
    }
</style>
