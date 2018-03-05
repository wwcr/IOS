<!--页面css样式-->
<style scoped>
    .nav{
        width: 80%;
        height: 1rem;
        border:1px solid #377bee;
        border-radius: 5px;
        margin: 0.5rem auto;
    }
    .nav li{
        border-right: 1px solid #377bee;
        font-size: 0.4rem;
        color: #377bee;
        width: 33%;
        float: left;
        height: 0.96rem;
        line-height: 0.96rem;
        text-align: center;
    }
    .nav li:last-child{
        border-right:none;
    }
    .nav li.cur{
        background: #377bee;
        color: #fff;
    }
    .list{
        width: 90%;
        margin: 0 auto;
        border-radius: 4px;
        position: relative;
    }
    .list ul em{
        width: 0.2rem;
        background: #f9d65f;
        position: absolute;
        left: 0;
        top: 0;
        height: 2.6rem;
        border-top-left-radius:4px;
        border-bottom-left-radius:4px;
    }
    .list ul li{
        height: 1.3rem;
        line-height: 1.3rem;
        text-align: center;
        width: 100%;
        background: #fff;
        color: #1e1e1e;
        font-size: 0.4rem;
    }
    .list ul li p{
        display: inline-block;
        float: left;
        width: 33%;
    }
    .con_list ul li p a{
        color: #e65e5e;
    }
    .ul_list{
        margin-bottom:0.4rem;
        position: relative
    }
    a{
        color: blue;
    }
</style>
<!--服务详情-->
<template>
    <div class="content">
        <ul class="nav" v-if="serverType==1">
            <li :class="{'cur':current[0]}" @click="currentChange(0)">看护中</li>
            <li :class="{'cur':current[1]}" @click="currentChange(1)">付款中</li>
            <li :class="{'cur':current[2]}" @click="currentChange(2)">已看护</li>
        </ul>
        <ul class="nav" v-if="serverType==2">
            <li :class="{'cur':current[0]}" @click="currentChange(0)">查找中</li>
            <li :class="{'cur':current[1]}" @click="currentChange(1)">付款中</li>
            <li :class="{'cur':current[2]}" @click="currentChange(2)">已找到</li>
        </ul>
        <ul class="nav" v-if="!serverType">
            <li :class="{'cur':current[0]}" @click="currentChange(0)">执行中</li>
            <li :class="{'cur':current[1]}" @click="currentChange(1)">未完成</li>
            <li :class="{'cur':current[2]}" @click="currentChange(2)">已完成</li>
        </ul>
        <div class="list">
            <ul v-for="x in list" class="ul_list">
                <em></em>
                <li><p>车牌号码</p><p>看护时间</p><p>车辆状态</p></li>
                <li>
                    <p>{{x.card_number}}</p>
                    <p>{{len(x.card_addtime)}}</p>
                    <p v-if="x.find_id"><a :href="'/server/list?sid='+serverType+'&id='+x.find_id">{{btnText}}</a></p>
                    <p v-else><a :href="'/server/list?sid='+serverType+'&id='+x.nurse_id">{{btnText}}</a></p>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
    import units from '../../tools/units'
    export default {
        name: 'index',
        data () {
            return {
                serverType:1,
                list: [],
                articlePage:0,
                articleLimit:6,
                moreThat:true,
                host:units.getHost(),
                current:[true,false,false],
                currentNum:1,
                sid:'',
                btnText:'执行中'
            }
        },
        methods: {
            len:function (str) {
                return str.substring(0,10);
            },
            currentChange:function (id) {
                this.current = [];
                for (let i = 0; i < 3; i++) {
                    if(i == id){
                        this.current.push(true);
                    }else{
                        this.current.push(false);
                    }
                }
                this.currentNum = id;
                this.list = [];
                this.articlePage = 0;
                if(id == 0){
                    this.getArticle(2);
                    this.btnText = '执行中'
                }else if(id == 1){
                    this.getArticle(1);
                    this.btnText = '未交接'
                }else{
                    this.getArticle(3);
                    this.btnText = '已交接'
                }
            },
            timeer:function (time) {
                return units.timemake(time)
            },
            more(){
                this.getArticle();
            },
            moreThatText:function () {
                return this.moreThat == true ? '查看更多' : '全部加载完成';
            },
            getArticle(status){
                let that = this;
                this.$http.post(units.host('server'),units.params({
                    type:that.serverType,
                    page:that.articlePage++,
                    sw:'content',
                    status:status,
                    limit:that.articleLimit
                })).then(function (res) {
                    let list =  res.data.info.data;
                    if(list.length < that.articleLimit)
                    {
                        that.moreThat = false;
                    }
                    for(let x in list){
                        that.list.push(list[x]);
                    }
                });
            }
        },
        created: function () {
            units.title.set('服务开启');
            this.serverType = this.$route.query.sid;
            this.$store.state.header.right = true;
            this.$store.state.header.rightTouch = function () {
                layer.msg('查找服务')
            };
            this.getArticle(2);
        }
    }
</script>