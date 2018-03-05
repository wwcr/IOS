<template>
    <div class="device-management-box" v-if='machineList.machine_num'>
        <div class="device-nav">
            <span @click="shotTab(0)" :class='{"curActive": curActiveFlag == 0}'><span class="text">拍摄总数量</span></span>
            <span @click="shotTab(1)" :class='{"curActive": curActiveFlag ==1}'><span class="text">报警拍摄总数</span></span>
        </div>
        <div class="device-content-box">
            <div class='device-content-page' v-show="currentID == 0">
                <div class="device-title"><b>拍摄总数量</b></div>
                <ul class="device-content">
                    <li class="device-content-li">
                        <span>寻车拍摄总数</span>
                        <span class="blue-color">{{machineList.statistics_machine.total_find_num}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近7天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.week_find_num}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近30天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.month_find_num}}</span>
                    </li>
                </ul>
            </div>  
            <div class='device-content-page' v-show='currentID == 1'>
                <div class="device-title"><b>已报警总数</b></div>
                <ul class="device-content">
                    <li class="device-content-li">
                        <span>报警拍摄总数</span>
                        <span class="blue-color">{{machineList.statistics_machine.total_num}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近7天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.week_num}}</span>
                    </li>
                    <li class="device-content-li">
                        <span>近30天拍摄数</span>
                        <span class="blue-color">{{machineList.statistics_machine.month_num}}</span>
                    </li>
                </ul>
            </div>  
        </div>

        <div class="photographing-num">
            <div><b>拍摄机共有{{machineList.machine_num}}台</b></div>
        </div>
        <div class="photographing-list-box">
            <div class="photographing-title">拍摄机列表</div>
            <div class="photographing-list">
                <div 
                    class="photographing-li"
                    v-for='(val, ind) in machineList.machine_list'
                    :key='ind'
                    >
                    <span><b>{{val.account}}</b><small>（{{val.mark}}）</small></span>
                    <span class="blue-color" @click="watchDetail(val.id)">查看</span>
                </div>
            </div>
        </div>

        <!-- 拍摄机详情弹出框 -->
        <div class="photographing-mark-box" v-if='closeShotFlag && machineDetails.data'>
            <div class="photographing-content">
                <div class="photographing-info">
                    <div class="user-name-box">
                        <div class="user-name" v-if='edit'>使用者名称：{{machineUser}}</div>
                        <div class="user-name" v-else>使用者名称：<input type="text" v-model="reviseName"></div>
                        <div class="edit" @click="editFn"><span v-if='edit'>编辑</span><span v-else>完成</span></div>
                    </div>
                    <div class="photographing-name">
                        拍摄机名称：{{machineDetails.data.account}}
                    </div>
                </div>
                <div class="shot-sum">
                    <div class="shot-sum-title"><b>拍摄总数</b></div>
                    <div class="shot-sum-box">
                        <div class="shot-sum-li">
                            <span>寻车拍摄总数</span>
                            <span class="grey-color">{{machineDetails.car_data.total_num}}</span>
                        </div>
                        <div class="shot-sum-li">
                            <span>近7天拍摄数</span>
                            <span class="grey-color">{{machineDetails.car_data.week_num}}</span>
                        </div>
                        <div class="shot-sum-li">
                            <span>近30天拍摄数</span>
                            <span class="grey-color">{{machineDetails.car_data.month_num}}</span>
                        </div>
                    </div>
                </div>
                <div class="shot-sum">
                    <div class="shot-sum-title"><b>已报警总数</b></div>
                    <div class="shot-sum-box">
                        <div class="shot-sum-li">
                            <span>已报警拍摄总数</span>
                            <span class="grey-color">{{machineDetails.car_data.total_find_num}}</span>
                        </div>
                        <div class="shot-sum-li">
                            <span>近7天拍摄数</span>
                            <span class="grey-color">{{machineDetails.car_data.week_find_num}}</span>
                        </div>
                        <div class="shot-sum-li">
                            <span>近30天拍摄数</span>
                            <span class="grey-color">{{machineDetails.car_data.month_find_num}}</span>
                        </div>
                    </div>
                </div>
                <div class="close-btn"><button @click="closeShotAlert(machineDetails)"></button></div>
            </div>
        </div>
    </div>
</template>

<script>
import units from '../../tools/units'
import cookie from '@/tools/cookie'
export default {
    name: 'devicemanagement',
    data () {
        return {
            currentID: 0,
            curActiveFlag: 0,
            machineUser: '我是傻子',//使用者的备注
            closeShotFlag: false, //拍摄机详情弹出框
            edit: true, //判断是否处于编辑状态
            user_id: '',
            machineList: {}, //大区经理设备统计接口
            machineDetails: {}, //每个设备详情
            everyId: 0, //每个设备机的id
            reviseName: '', //修改后的名字
        }
    },
    methods: {
        shotTab (id) { //Tab切换
            this.currentID = id;
            this.curActiveFlag = id
        },
        watchDetail (id) { //查看每一台摄像机详情
            this.everyId = id
            this.$http.post(units.domin('Hardware/machineInfo'), { id }).then( function (res) {
                if (res.ok) {
                    this.machineDetails = res.body.info
                    this.machineUser = this.machineDetails.data.mark
                    this.closeShotFlag = true
                }
            })
        },
        editFn () {//编辑备注
           if(this.edit) {
               this.edit = false
           } else {
               this.$http.post(units.domin('Machines/updateMachine'), {
                    id:this.everyId,
                    switch:'savemark',
                    mark: this.reviseName
                }).then( function (res) {
                    if (res.ok) {
                        console.log(res)
                        layer.msg(res.body.msg)
                        this.machineUser = this.reviseName
                        this.reviseName = ''
                    }
                })
               this.edit = true
           }
        },
        closeShotAlert (detail) { //关闭拍摄机详情弹出框
            this.closeShotFlag = false;
            this.getMachineData ()
        },
        getMachineData () { //大区经理设备统计接口数据
            this.$http.post(units.domin('Machines/statisticsMachine'), {
                role:1,
                uid:this.user_id,
            }).then( function (res) {
                if (res.ok) {
                    this.machineList = res.body.info
                }
            })
        }
    },
    created () {
        units.title.set('设备详情');
        this.user_id = cookie.get('user_id')
        this.getMachineData ()
    }
}
</script>

<style scoped lang='scss'>
    .blue-color{
        color: #3d87ff;
        font-weight: bolder;
        vertical-align: bottom;
    }
    .grey-color{
        color: #787878;
        vertical-align: bottom;
    }
    .device-management-box{
        padding-top: 1.31rem;
        font-size: .45rem;
        .device-nav{ //导航
            display: flex;
            background: #fff;
            span{
                flex:1;
                border: .01rem solid #f2f6f7;
                text-align: center;
                &:nth-child(1){
                    border:0;
                }
                &.curActive span{
                    border-bottom: .06rem solid #3d7fed;
                }
                .text{
                    display: inline-block;
                    padding: .2rem 0;
                    border-bottom: .06rem solid #fff;
                }
            }
        }
        .device-content-box{  //拍摄/报警的详细内容
            margin-top: .35rem;
            .device-title{
                line-height: 1.3rem;
                padding: 0  .5rem; 
                box-sizing: border-box;
                font-size: .5rem;
            }
            .device-content{
                background: #fff;
                width: 100%;
                padding-bottom: .7rem; 
                li{
                    padding: 0  .5rem; 
                    padding-top: .7rem; 
                    box-sizing: border-box;
                    display: flex;
                    justify-content: space-between;
                }
            }
        }
        .photographing-num{ //拍摄机总数
            line-height: 2rem;
            text-align: center;
            color: #ff671c;
            background: #fff;
            padding: 0  .5rem;
            box-sizing: border-box;
            div{
                border-top: .01rem solid #eeeeee;
                font-size: .5rem;
            }
        }
        .photographing-list-box{ //拍摄机列表
            margin-top: .35rem;
            .photographing-title{
                line-height: 1.3rem;
                padding: 0  .5rem; 
                box-sizing: border-box;
                font-size: .5rem;
            }
            .photographing-list{
                background: #fff;
                .photographing-li{
                    display: flex;
                    justify-content: space-between;
                    margin: 0 .5rem;
                    padding: .4rem 0;
                    border-bottom: .01rem solid #eeeeee;
                }
            }
        }
        .photographing-mark-box{//拍摄机详情弹出框
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0, 0.5);
            z-index: 999;
            .photographing-content{
                margin: 10% 0 0 50%;
                transform: translate(-50%);
                background: #fff;
                width: 8.5rem;
                height: 15rem;
                border-radius: .1rem;
                .photographing-info{
                    box-sizing: border-box;
                    padding:  0 .6rem;
                    .user-name-box{
                        display: flex;
                        justify-content: space-between;
                        padding-top: .6rem; 
                        .user-name{
                            input{
                                border:.01rem solid #ccc;
                                width: 2.2rem;
                                height: .6rem;;
                            }
                        }
                    }
                    .edit{
                        color: #ff671c;
                    }
                    .photographing-name{
                        padding:  .35rem 0;
                    }

                }
                .shot-sum{//拍摄机总数
                    .shot-sum-title{
                        box-sizing: border-box;
                        padding: .4rem .6rem .1rem .6rem;
                        line-height: 1rem;
                        background: #f0f4fa;
                    }
                    .shot-sum-box{
                        box-sizing: border-box;
                        padding:0 .6rem;
                        padding-bottom: .5rem;
                        .shot-sum-li{
                            padding-top: .5rem;
                            display: flex;
                            justify-content: space-between;
                        }
                    }
                }
            }
            .close-btn{
                width: 100%;
                height: 1.9rem;
                text-align: center;
                background: #f0f4fa;
                border-radius: .1rem;
                button{   
                    margin-top: .4rem;
                    width: 7.3rem;
                    height:1.3rem;
                    border: 0;
                    outline: none;
                    background: url(../../assets/img/close-btn.png) no-repeat center;
                    background-size: 100%;
                }
            }
        }
    }
</style>
