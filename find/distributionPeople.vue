<template>
    <div class="distribution-box">
        <div class="header">
           <a href="javascript:history.go(-1);" class="go_return"></a>
           <p class="title">分配人员</p>
           <a class="right_btn" @click="sure()">
               确定
           </a>
       </div>
        <ul class="distribution-content">
            <li
                v-for='(val, ind) in info'
                :key='ind'
                @click='checkPeo(val)'
                v-if='form.single_order.card_uid != val.user_id'
            >
                 <div class="info-content">
                    <div class="header-img"><img src="../../assets/img/header-img.png" alt=""></div>
                    <div class="conten-box">
                        <p class="title" v-if='val.per_name'>{{val.per_name}}</p>
                        <p class="title" v-else>{{val.enuser_name}}</p>
                        <p class="content" v-if='val.per_address'>{{val.per_address}}</p>
                        <p class="content"  v-else>{{val.enuser_address}}</p>
                    </div>
                </div>
                <div class="check-one">
                    <input type="radio"  value="1" id="checkbox1"  name='fenpei'>
                    <label for="checkbox1"></label>
                </div>
            </li>
        </ul>
        <dialogBox 
            v-show='dialogFlag'
        />
    </div>
</template>

<script>
   import units from '../../tools/units'
   import dialogBox from './dialogBox'
import cookie from '../../tools/cookie'
export default {
    name: 'distributionPeople',
    data () {
        return {
            dialogFlag: false,
            info: [],
            a: false,
            form: {
                single_order:'',//订单id
                single_uid: '',//大区经理
                user_id: ''//用户
            }
        }
    },
    methods: {
        
        checkPeo (val) {
            // console.log(val,111)
            this.form.user_id = val.user_id
        },
        sure () {
            this.dialogFlag = true
            this.form.single_uid = cookie.get('user_id')
            
            console.log(this.form.single_order,this.form.single_uid,this.form.user_id)
            this.$http.post(units.host('assignOrderToUser'), {
                single_order: this.form.single_order.ex_oid,
                single_uid: this.form.single_uid,
                user_id: this.form.user_id
            }).then(function (res) {
                this.info = res.body.info
            });
            setTimeout (() =>{
                    this.dialogFlag = false
                    this.$router.push({
                        path: '/find/index',
                        query: {
                            id:2,
                            current: 1
                        }
                    })
            }, 2000)
        },
        getData (userID) {
            this.$http.post(units.host('proxyUserBelogUsers'), {//大区经理的所有用户
                user_id:userID
            }).then(function (res) {
                this.info = res.body.info
                console.log(this.info);
            });
        }
    },
    created () {
        
        var userID = cookie.get('user_id');
        this.getData (userID);
        this.form.single_uid = userID
        this.form.single_order = this.$route.query.id;

    },
    components: {
        dialogBox
    }
}
</script>

<style scoped lang='scss'>
    .distribution-box{
        width: 100%;        
        font-size: .38rem;
        .distribution-content{
            background: #f0f4fa;
            padding-top: 1.65rem;
            li{
                background: #fff;
                border-bottom: .01rem solid #f0f4fa;
                box-sizing: border-box;
                padding: .4rem;
                display: flex;
                justify-content: space-between;
                .header-img{
                    width: 1.5rem;
                    height: 1.5rem;
                    img{
                        width: 100%;
                    }
                }
                .info-content{
                    display: flex;
                    .content{
                        color: #787878;
                    }
                    .conten-box{
                        margin-left:.5rem; 
                        p{
                            margin-top:.1rem; 
                        }
                        .title{
                            font-size: .38rem;
                            font-weight: bold;
                            color: #000;
                        }
                    }
                }
            }
        }
    }
    .check-one {  
    // width: 25px;  
    // margin: 20px 100px;  
    position: relative;  
    }  
    .check-one input[type=radio] {  
        // visibility: hidden;  
        position: relative;
        top: .5rem;
        z-index: 999;
        // width: 1rem;
        // height: 1rem;
    }  
    // .check-one label {  
    //     cursor: pointer;  
    //     position: absolute;  
    //     width: .55rem;  
    //     height: .55rem;  
    //     background: #fff;  
    //     border:.02rem solid #ccc;  
    //     -moz-border-radius: 50%;      /* Gecko browsers */  
    //     -webkit-border-radius: 50%;   /* Webkit browsers */  
    //     border-radius:50%;    
    //     right: .01rem;        /* W3C syntax */  
    // }  
    // .check-one label:after {  
    //     opacity: 0;  
    //     content: '\2714';  
    //     font-size: .2rem;
    //     text-align: center;
    //     position: absolute;  
    //     width: .52rem;  
    //     height: .52rem; 
    //     border-radius: 50%;
    //     line-height: .43rem;    
    //     background: #2c7dfe;
    //     color: #fff;
    //     top: 0;  
    //     left: 0; 
    // } 
    // .check-one input[type=radio]:checked + label:after {  
    //     opacity: 1;
    // }  
</style>
