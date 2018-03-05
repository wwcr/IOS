<template>
    <div class="calcultor-box">
        <div class="calcutor-sum-box">
            <div class="calcutor-sum">
                <div class='sum-top'>
                    <p>预计花费总额（元）</p>
                    <p class='sum-price'><b>116,944,00</b></p>
                    <p>比全款购车多花2,,516,00</p>
                </div>
                <div class='every-sum'>
                    <div class='every-price'>
                        <p >首期支付金额</p>
                        <p>44,425,00</p>
                    </div>
                    <div class='every-price'>
                        <p>首期支付金额</p>
                        <p>44,425,00</p>
                    </div>
                    <div class='every-price'>
                        <p>首期支付金额</p>
                        <p>44,425,00</p>
                    </div>
                </div>
            </div>
            <div class="horn-box">
                <img src="../../src/assets/img/icon-laba.png" alt="">
                <span>计算结果已加入购置税、车船使用税/交强险、上牌费</span>
            </div>
        </div>
        <div class='check-box'>
            <ul>
                <li>
                    <span>购买价格</span>
                    <input 
                        type='text' 
                        placeholder='0'
                        v-model='calInfo.buyPrice'
                    />
                    <small>元</small>
                </li>
                <li>
                    <span>首付额度</span>
                    <input 
                        type='text' 
                        placeholder='0%'
                        v-model='calInfo.startPrice'
                    />
                    <small><img src='../../src/assets/img/down-jt.jpg'></small>
                </li>
                <li>
                    <span>首期支付</span>
                    <input type='text' placeholder='0'>
                    <small>元</small>
                </li>
                <li>
                    <span>首付额度</span>
                    <input type='text' placeholder='0%'>
                    <small><img src='../../src/assets/img/down-jt.jpg'></small>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
import units from '@/tools/units'
export default {
    name: 'CarCalculator',
    data () {
        return {
            calInfo: {
                buyPrice: '',
                startPrice: '',

            }
        }
    },
    created () {
        units.title.set('车贷计算器');
    }
}
</script>
<style lang='scss' scoped>
    .calcultor-box{
        padding-top: 1.25rem;
        font-size: .4rem;
        background: #f0f4fa;
        .calcutor-sum-box{
            background: #fff;
            padding: .4rem;
            box-sizing: border-box; 
            .calcutor-sum{
                width: 100%;
                height: 5.5rem;
                color: #fff;
                text-align:center;
                // background: url(../../src/assets/img/aa.png) no-repeat;
                // background: url(../../src/assets/img/but_1.png);
                background: #3787fe;
                border-radius: .2rem;
                background-size: 100%;
                .sum-top{
                    p{
                        padding-top: .3rem;
                    }
                }
                .sum-price{
                    font-size: .6rem;
                }
                .every-sum{
                    border-top: .01rem solid #b8c1ce;
                    box-sizing:border-box;
                    margin: 0 .4rem;
                    margin-top: .4rem;
                    padding: .5rem;
                    display:flex;
                    justify-content: space-around;
                    .price{
                        font-weight: bold;
                    }
                    .title{
                        font-size: .45rem;
                    }
                }
            }
            .horn-box{
                padding: .4rem 0;
                img{
                    width: .5rem;
                }
            }
        }
        .check-box{
            background: #fff;
            ul {
                margin-top: .4rem;
                li{
                    display: flex;
                    justify-content: space-between;
                    padding:0 0.3rem;
                    border-bottom: .01rem solid #dcdcdc;
                    margin: 0 .4rem;
                    box-sizing: border-box;
                    line-height: 1.5rem;
                    input{
                        text-align: right;
                        position: relative;
                        right: -1.5rem;
                        width: 4rem;
                        top: .2rem;
                        height: 1.2rem;
                    }
                    small{
                        img{
                            width: .3rem;
                        }
                    }
                }
            }
        }
        
    }
</style>

