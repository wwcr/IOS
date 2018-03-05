<template>
    <div class="history-page">
        <div class="peccancy-detail-box-content">
            <div class="peccancy-detail-title">
                <span class="times-box">
                    <span class="data">2016-09-06</span>
                    <span class="time">20:00</span>
                </span>
                <span class="plate-num">京A88888</span>
            </div>
            <h4 class="peccancy-title">违规内容</h4>
            <p class="detail-content">北京朝阳望京街道快速道路上驾驶，闯红灯</p>
            <p class="detail-address"><span><img src="../../../assets/img/address-icon.png" alt=""></span>北京朝阳望京东</p>
            <div class="detail-content-item">
                <span>未处理</span>
                <span>扣分6</span>
                <span>罚款<small>¥50 </small></span>
            </div>
        </div>
    </div>
</template>
<script>
import units from '@/tools/units'
export default {
    name: 'history',
    created () {
        this.$store.state.header.right = false
        units.title.set('历史记录');
    }
}
</script>
<style scoped lang='scss'>
    .history-page{
        background: #f0f4fa;
        padding-top:1.25rem;
        font-size:.5rem;
         .peccancy-detail-box-content{
            padding: 0 .35rem;
            margin-top: .4rem; 
            background: #fff;
            .peccancy-detail-title{
                font-size: .4rem; 
                color: #b4b4b4;
                line-height: 1.5rem;
                display: flex;
                justify-content: space-between;
                .time{
                    margin-left:.2rem;
                    line-height: 1.5rem; 
                }
                .plate-num{
                    color: #000;
                }
            }
            .detail-content{
                color:#818181;
            }
            .detail-address{
                color:#b4b4b4;
            }
            .peccancy-title{
                font-size:.6rem;
            }
            p{
                line-height: 1rem; 
            }
            .detail-address{
                img{
                    width: .4rem;
                    height: .54rem;
                    position: relative;
                    top: -.08rem;
                    margin-right: .2rem;
                }
            }
            .detail-content-item{
                width: 100%;
                display: flex;;
                padding-bottom:.5rem; 
                margin-top:.3rem; 
                span{
                    flex:1;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    border-right:0.01rem solid #f0f0f0;
                    &:nth-child(3){
                        border:0;
                    }
                     
                    small{
                        color: red;
                        margin-left:.2rem; 
                        font-size:.501rem;
                    }
                }
            }

        }
    }
</style>

