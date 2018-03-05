<template>
    <div class="city-page-box" v-if='modelList'>
        <div class="city-title">车型<span class="closeBtn" @click="checkCityFn(1)">×</span></div>
        <div class="wrapper" ref='wrapper'>
            <div class="content">
                <ul class="city-content">
                    <li
                        v-for='(val,ind) in modelList'
                        :key='ind'
                        @click='checkCityFn(val)'
                    >
                        <span>{{val.cxname}}</span>
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
    props: ['modelList'],
    methods: {
        checkCityFn (val) {
            this.$emit('closeModel', val)
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
        width: 40%;
        font-size: .3rem;
        position: fixed;
        background: #fff;
        right:0;
        top:0rem;
        bottom: 0;
        z-index: 1000;
        .city-title{
            padding:.2rem;
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
            z-index: 1000;
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
                padding: .1rem 0;
                line-height: .5rem;
            }
        }
    }
</style>
