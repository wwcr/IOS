<!--设置-->
<template>
    <div class="setting">
        <div style="padding-top: 1.7rem;background:#f8f9fa;">
            <div class="in_list">
                <ul>
                    <li style="height:2rem;">
                        <a style="line-height:2rem;">
                            <label style="line-height: 1.8rem;">头像</label>
                            <span style="margin-top: 0.25rem;" class="arrow_right"></span>
                            <span class="message" style="position:relative">
                                <input style="position: absolute;width:100%;opacity:0" type="file" name="" @change="upload()">
                                <img v-if="!thumb" src="../../../src/assets/img/img_img1.png">
                                <img :src="thumb" v-else>
                            </span>
                        </a>
                    </li>
                    <li v-if="false">
                        <a @click="href('user/nickname?t='+info.user_nickname)">
                            <label>昵称</label>
                            <span class="arrow_right"></span>
                            <span class="message">
                <input type="text" class="text" v-model="info.user_nickname" readonly>
                </span>
                        </a>
                    </li>
                </ul>
            </div>
            <div class="in_list">
                <ul>
                    <li>
                        <a href="#/user/reset">
                            <label>修改密码</label>
                            <span class="arrow_right"></span>
                            <span class="message">
                <input type="text" class="text" readonly>
                </span>
                        </a>
                    </li>
                    <li v-if="false">
                        <a @click="delCache()">
                            <label>清理缓存</label>
                            <span class="arrow_right"></span>
                            <span class="message">
                <input type="text" class="text" readonly>
                </span>
                        </a>
                    </li>
                    <li>
                        <a @click="href('user/aboutus')">
                            <label>关于我们</label>
                            <span class="arrow_right"></span>
                            <span class="message">
                <input type="text" class="text" readonly>
                </span>
                        </a>
                    </li>
                </ul>
            </div>
            <div class="exit" @click="exiter()">退出当前账号</div>
        </div>
    </div>
</template>
<script type="text/javascript">
    import units from '../../tools/units'
    import lrz from '../../../static/lrz/lrz.bundle'
    import cookie from '../../tools/cookie'
    export default {
        name: 'index',
        data () {
            return {
                thumb:'',
                info:{}
            }
        },
        methods: {
            chose: function (id) {
            },
            upload: function () {
                let e = event;
                let that = this;
                let reader = new FileReader();
                reader.readAsDataURL(event.target.files[0]);
                reader.onload = function() {
                    let imgs = this.result;
                    that.thumb = URL.createObjectURL(e.target.files[0]);
                    that.Http('units/imgstr',{
                        imgstr:imgs
                    },function (res) {
                        layer.msg(res.msg,2,function () {
                            if(res.code > 0){
                                that.Http('user/updateHeader',{
                                    header:res.info
                                },function(up){
                                    if(up){
                                        layer.msg(up.msg,2,function () {})
                                    }else{
                                        layer.msg('更新失败');
                                    }
                                })
                            }
                        })
                    })
                };
            },
            getinfo:function () {
                let that = this;
               this.Http('user/info',{},function (res) {
                   that.info = res.info;
                   if(res.info.user_header){
                       that.thumb =  units.getHost() + res.info.user_header
                   }
               })
            },
            exiter:function () {
                let that = this;
                layer.tips(["是","否"],'',function (e) {
                    if(e == '是'){
                        localStorage.removeItem("isVIP")
                        cookie.del('user_id');
                        cookie.del('user_nickname');
                        cookie.del('user_token');
                        cookie.del('role')
                        cookie.del('c_status')
                        cookie.del('sign_uesr')
                        cookie.del('findIndexCur')
                        layer.msg('退出成功',3,function () {
                            that.href('login')
                        })
                    }
                });
            },
            delCache:function () {
                layer.loading('清理中...');
                new Promise(function () {
                    setTimeout(function () {
                        layer.loading(false);
                        layer.msg('清理完成')
                    },1000)
                })
            }
        },
        created: function () {
            units.title.set('设置');
            this.getinfo();
        }
    }
</script>
<!--页面css样式-->
<style scoped>
    .in_list {
        background: #fff;
        border-top: 1px solid #f1f1f1;
        border-bottom: 1px solid #f1f1f1;
        /* margin-top: 0.3rem; */
        /* padding-top:1.3rem;  */
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
        font-size: 0.48rem;
        color: #1e1e1e;
    }

    .in_list .message {
        position: relative;
        float: right;
        margin: 0;
        height: auto;
        width: 70%;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        color: #d3d5dc;
        font-size: 0.48rem;
        line-height: 1.48rem;
        display: inline-block;

    }

    .in_list .message input {
        border: none;
        background: none;
        font-size: 0.48rem;
        color: #1e1e1e;
        -webkit-tap-highlight-color: transparent;
        /* font-family: "微软雅黑"; */
        /* font-family: 'Droidsansfallback'; */
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
        text-align: right;
    }

    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background: url(../../../src/assets/img/img_14.png) no-repeat;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .in_list li a .arrow_right_2 {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background-position: right center;
        background-size: auto 30%;
        float: right;
    }

    .message img {
        width: 1.5rem;
        height: 1.5rem;
        float: right;
        margin-top: 0.25rem;
        border: 1px solid #cbd6e8;
        border-radius: 50%;
    }

    .exit {
        height: 1.45rem;
        line-height: 1.45rem;
        text-align: center;
        color: #fd2121;
        background: #fff;
        margin-top: 0.3rem;
        font-size: 0.48rem;
    }
</style>