<template>
    <div class="peccancy-detail-box">
        <div 
            v-if='peccancyData.dataList.province'
            class="peccancy-detail-box-content"
            v-for='(value, index) in peccancyData.dataList.lists'
            :key='index'
            >
            <div class="peccancy-detail-title">
                <span class="data">{{value.date}}</span>
            </div>
            <h4 class="peccancy-title">违规内容</h4>
            <p class="detail-content">{{value.act}}</p>
            <p class="detail-address"><span><img src="../../../assets/img/address-icon.png" alt=""></span>{{value.wzcity}}{{value.area}}</p>
            <div class="detail-content-item">
                <span style='color:red' v-if='value.handled*1'>已处理</span>
                <span v-else>未处理</span>
                <span>扣分{{value.fen}}</span>
                <span>罚款<small>¥{{value.money}} </small></span>
            </div>
        </div>
    </div>
</template>
<script>
import units from '@/tools/units'
export default {
    name: 'PeccancyDetail',
    data () {
        return {
            peccancyData: {},
            processFlag: 1
        }
    },
    created () {
      this.$nextTick(() => {
          this.peccancyData = this.$route.query
          units.title.set(this.peccancyData.hphm);
      })
      
  }
}
</script>
<style lang='scss' scoped>
    .peccancy-detail-box{
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
                line-height: 1rem;
                padding-top:.2rem; 
            }
            .detail-content{
                color:#818181;
                font-size: .4rem;
                line-height: .7rem;
            }
            .detail-address{
                color:#b4b4b4;
                margin-top: .2rem;
                font-size: .4rem;
            }
            .peccancy-title{
                font-size:.6rem;
                margin-bottom:.4rem; 
            }
            p{
                line-height: .8rem; 
            }
            .detail-address{
                img{
                    width: 0.35rem;
                    height: .44rem;
                    position: relative;
                    top: -.03rem;
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
                    &:nth-child(1){
                        color: #5999ff;
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
