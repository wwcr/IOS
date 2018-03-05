<!--页面css样式-->
<style scoped>
    .per_top {
        width: 100%;
        position: relative;
    }

    .per_top div.header-bg {
        /*background: url("../../assets/img/img_38.png") no-repeat;*/
        background-size: auto 100%;
        background-origin: border-box;
        background-position: center center;
        height: 2.8rem;
    }

    .per_top img {
        width: 100%;
        height: 6.63rem;
    }

    .per_top p {
        position: absolute;
        color: #fff;
        bottom: 1.3rem;
        left: 31%;
        font-size: 0.4rem;
        width: 37%;
        text-align: center;
    }

    .per_top div {
        width: 50%;
        margin: 0 auto;
        position: absolute;
        top: 25%;
        left: 25%;
        text-align: center;
    }

    .per_top div img {
        width: 2.2rem;
        height: 2.2rem;
        line-height: 2.8rem;
        border-radius: 50%;
        display: block;
        margin: 0 auto;
        margin-top: 0.3rem;
    }

    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
        margin-top: 0.3rem;
    }

    .in_list:last-child {
        border-bottom: none;
    }

    .in_list li {
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        margin-left: 0.4rem;
    }

    .in_list li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        height: 1.49rem;
        line-height: 1.49rem;
        min-height: 1.49rem;
    }

    .in_list li a label {
        font-size: 0.4rem;
        color: #1e1e1e;
    }

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 50%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        line-height: 1.48rem;
        display: inline-block;

    }

    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.7rem;
        height: 1.48rem;
        background: url(../../assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.7rem;
        height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a img {
        width: 0.4rem;
        vertical-align: middle;
        margin-top: 0.1rem;
    }

    .message p {
        font-size: 0.4rem;
        color: #1e1e1e;
        width: 40%;
    }

    .message p.p_p1 {
        color: #e24a4a;
    }

    .message p {
        text-align: right;
        float: right;
        width: 100%;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    .setting{
        position: absolute;
        right: 0.6rem;
        top: 0.4rem;
        color: #ffffff;
        font-size: 0.4rem;
    }

</style>
<!--个人中心-->
<template>
    <div class="personal">
        <div class="per_top">
            <span class="setting" @click="href('user/setting')">设置</span>
            <img src="../../assets/img/img_37.jpg">
            <div class="header-bg" v-if="info.user_header">
                <img style="border-radius:50%" :src="host+info.user_header">
            </div>
            <div class="header-bg" v-else>
              <img src="../../assets/img/img_38.png">
            </div>
            <p @click="outUser">{{info.user_mobile}}</p>
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <img src="../../../src/assets/img/group_icon.png">
                        <label>资料认证</label>
                        <span v-if="info.user_anthen != 0">
                            <span class="arrow_right"></span>
                            <span class="message">
                                <p>已认证</p>
                            </span>
                        </span>
                        <span v-else>
                            <span class="message">
                                <a @click="href('Metype')"><p>未认证</p></a>
                            </span>
                        </span>
                    </a>
                </li>
                <!-- <li>
                    <a @click="href('user/firmname?t='+info.auth.per_workunit)">
                        <img src="../../../src/assets/img/group_icon2.png">
                        <label>企业名称</label>
                        <span class="arrow_right"></span>
                        <span class="message" v-if="info.auth != null || info.auth != undefined">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span>
                    </a>
                </li> -->
                <li v-if="isVIP">
                    <a @click="href('user/myteam')">
                        <img src="../../../src/assets/img/group_icon8.png">
                        <label>员工管理</label>
                        <span class="arrow_right"></span>
                        <!-- <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span> -->
                    </a>
                </li>
                <li v-if="isVIP">
                    <a @click="href('user/datacollection')">
                        <img src="../../../src/assets/img/group_icon7.png">
                        <label>数据总览</label>
                        <span class="arrow_right"></span>
                        <!-- <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span> -->
                    </a>
                </li>
                <li v-else>
                    <a @click="href('user/ordercount')">
                        <img src="../../../src/assets/img/group_icon7.png">
                        <label>订单统计</label>
                        <span class="arrow_right"></span>
                        <!-- <span class="message" v-if="info.auth != null">
                            <p v-if="info.auth.per_workunit">{{info.auth.per_workunit}}</p>
                            <p v-else>{{info.auth.en_name}}</p>
                        </span> -->
                    </a>
                </li>
                <li v-if="false">
                    <a>
                        <img src="../../../src/assets/img/group_icon3.png">
                        <label>员工职位</label>
                        <span class="arrow_right_2"></span>
                        <span class="message" v-if="info.auth">
                            <p>{{info.auth.per_worker||'暂无'}}</p>
                        </span>
                        <span v-else>
                            <a @click="href('authentication')">未认证</a>
                        </span>
                    </a>
                </li>
                <li v-if="false">
                    <a>
                        <img src="../../../src/assets/img/group_icon4.png">
                        <label>设置捆绑</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                            <p class="p_p1" onclick="layer.msg('正在进行中,请稍等...')">开始捆绑</p>
                        </span>
                    </a>
                </li>
                <li v-if="false">
                    <a>
                        <img src="../../../src/assets/img/group_icon5.png">
                        <label>设备状态</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                           <p class="p_p1" onclick="layer.msg('正在准备中,请稍等...')">查看</p>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <img src="../../../src/assets/img/group_icon6.png">
                        <label>客服电话</label>
                        <span v-if="info.user_anthen != 0">
                  <span class="arrow_right_2"></span>
                  <span class="message">
                    <p>010-84685465</p>
                  </span>
                </span>
                        <span v-else>
                 <span class="message">
                   <a ><p style="color:#b4b4b4">010-84685465</p></a>
                 </span>
               </span>
                    </a>
                </li>
            </ul>
        </div>
        <navcate></navcate>
    </div>
</template>
<script>
    import units from '../../tools/units'
    import isVIP from '../../tools/isVIP'
    import cookie from '../../tools/cookie'
    import navcate from '../template/navcate.vue'
    export default {
        name: 'index',
        data () {
            return {
                info: {
                    auth: {}
                },
                isVIP: false  //是否大堂经理
            }
        },
        components: {
            navcate
        },
        methods: {
            outUser: function () {
                let that = this;
                layer.open({
                    content: '退出当前账号',
                    btn: ['退出账号', '切换账号'],
                    yes: function () {
                        that.delCook(function () {
                            location.href = '/login';
                        });
                    },
                    no: function () {
                        that.delCook(function () {
                            location.href = '/';
                        });
                    }
                });
            },
            delCook: function (fn) {
                cookie.del('user_id');
                cookie.del('user_nickname');
                cookie.del('user_token');
                fn & fn();
            },
            len: function (str) {
                return str.substring(0, 10);
            },
            getdata: function () {
                this.$http.post(units.host('user'), units.params({
                    sw: 'info'
                })).then(function (res) {
                    console.log(res.data.info.user_anthen)
                    cookie.set('user_auth', res.data.info.user_anthen)
                    this.info = res.data.info;
                });
            }
        },
        created: function () {
            this.getdata();
            units.title.set('个人中心');
            units.isLogin(true);
            if(localStorage.getItem("isVIP")){
                this.isVIP = localStorage.getItem("isVIP")
                console.log(this.isVIP)
            } else {
                this.isVIP = this.$store.state.isVIP
            }
        },
        beforeCreate: function () {
        },
    }
</script>
