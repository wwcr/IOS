 <template>
<div>
   <img :src="pic" style="width:100%;">
</div>
    <!-- <div class="contract-box">
        <p></p>
        <p>放心签字，当双方交车时，此协议会自动销毁</p>
        <p>甲方因本人生产或经营需要，向乙方申请借款，并以自有车辆作为抵押物，经当事方协商一致，乙方同意出借并签定本合同内容。</p>
        <p>第一项 借款事项</p>
        <p>第一条 借款内容</p>
        <p>借款总金额：人民币 _______元，大写 _______________.</p>
        <p>借款期限：自 年 月 日起至 年 月 日止，共计 _____天。月利息 _______.</p>
        <p>第二条 借款的支付及偿还</p>
        <p>1. 借款的支付：借款及抵押手续办妥后，乙方将借款金额一次性支付给甲方或转入甲方账户。</p>
        <p>2. 借款的偿还：本借款在到期日一次性还清本息。</p>
       <p> 3. 甲方可以提前还款，但必须提前15天通知乙方。</p>
        <p>第三条 违约责任</p>
        <p>1. 如果甲方到期不能全额偿还本借款，则从逾期之日起，对未偿还部分加收 /天 的违约金，逾期超过十日的，视为甲方彻底违约，乙方可以解除本借款合同，要求甲方支付合同总借款金额20%的违约金；</p>

        <p>1. 抵押物由乙方保管， 在抵押期间，乙方无偿使用该车辆，保证该车辆无任何交通事故及违章。若是由于车辆自身原因或自然损坏，不可抗力等因素造成的车辆损失，免除乙方赔偿责任。</p>
        <p>2. 甲方必须连同与抵押车辆相关的钥匙、机动车登记证书、行车证、购车发票、购置税、养路费、保险单据、户口本原件及身份证复印件交由乙方或中间人保管。</p>
        <p>第七条 抵押物的处置</p>
        <p>1.抵押期间，甲方对抵押车辆做出的任何处置均无效。</p>
        <p>2.甲方如不能按时还款，自逾期 天后，乙方则可以变卖抵押物以挽回损失，甲方同时签署《逾期变卖委托书》。</p>
        <p>第八条 抵押期间，发生下列情形之一，乙方有权提前处置抵押物</p>
        <p>1.借款人被宣告失踪，而其财产代管人拒绝履行本合同的；</p>
        <p>2.借款人丧失民事行为能力，而监护人拒绝履行本合同的；</p>
        <p>3.借款人死亡或宣告死亡而其财产合法继承人拒绝履行本合同的；</p>
        <p>4.借款人不履行还款义务或有其他缺乏偿债诚意的行为；</p>
        <p>5.借款人卷入或将卷入重大的诉讼或仲裁程序及其他法律纠纷，足以影响其偿债能力；</p>
        <p>6.借款人变更住所。通信地址。联系电话等事项未在5日内及时通知的。</p>
        <p>第三项 其它规定</p>
        <p>第九条 费用的承担</p>
        <p>1.如果甲方不能按期还款，在争取乙方同意的情况下可以展期。</p>
        <p>2.有关抵押、借款产生的一切费用均由甲方承担。</p>
        <p>第十条 本合同生效条件</p>
        <p>本合同自当事人签字之日起生效。</p>
        <p>本合同一式 份，甲方、乙方各执一份，其余在有关部门备案。</p>
        <p>甲方：_______________（借款人）</p>
              
         <p>乙方签字：</p>
         <p style="width:2rem;height:2rem;"  v-on:click='test()'></p>
         <p style="color:red;margin-left:2.8rem;font-size:.3rem;">放心签字，当双方交车时，此协议会自动销毁</p>                          
                


              

         
    </div> -->
</template>

<script>
import units from '../tools/units';
 import cookie from '../tools/cookie'
export default {
    name: 'contract',
    data () {
            return {
                car_addtime:'',
                car_location:'',
                pic:'',
            }
        },
    created () {
        units.title.set('电子合同');
        this.$store.state.header.left = function () {
            location.href = '#/findcar';
        };
        
    },
    mounted(){
                var uid = cookie.get('user_id');
                this.$http.post(units.host('get_userinfo','api'), {
                    uid: uid//穿车牌
                }).then(function (res) {
                  this.pic = units.getHost() + res.body.contract;
                });
    },
    methods: {
    test: function () {
      alert(111);
      location.href = '#/sign'
    }
  }
}
</script>

<style lang='scss' scoped>
    .contract-box{
        font-size: .4rem;
        padding:1.25rem .5rem .2rem .5rem; 
        p{
            line-height: .8rem;
        }
    }
</style>
