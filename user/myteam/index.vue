<template>
    <div class="my-team-box">
        <ul>
            <template v-for = '(val, ind) in userTeam'>
                <li
                    :key='ind'
                >
                    <span class="team-name">{{val.user_nickname}}</span>
                    <span
                        class="team-status"
                        @click='seeFn(val)'
                    >查看</span>
                </li>
            </template>
        </ul>
    </div>
</template>

<script>
import units from '../../../tools/units'
export default {
    name: 'myteam',
    data() {
        return {
            userTeam:{},
        }
    },
    methods: {
        seeFn (val) {
            console.log('查看',val)
            this.$router.push('/user/teamstatus?each_user='+val.user_id)
        },

        getUserTeamList:function () {
            this.$http.post(units.host('userTeamList'), units.params({
                switch: 'user_team',
            })).then(function (res) {
                this.userTeam = res.data.info;
                // console.log(res.data.info);
            });
        },
    },

    created: function () {
        units.title.set('员工管理');
        this.getUserTeamList();
    },
}
</script>

<style scoped lang='scss'>
    .my-team-box{
        width:100%;
        padding-top:1.25rem;
        background: #f0f4fa;
        font-size: .44rem;
        ul{
            background: #fff;
            margin-top: .38rem;
            li{
                border-bottom: .01rem solid #f0f4fa;
                box-sizing: border-box;
                padding:0 .4rem;
                display: flex;
                line-height: 1.1rem;
                justify-content: space-between;
                .team-status{
                    color: #2c7dfe;
                    font-size: .3rem;
                }
            }
        }
    }
</style>
