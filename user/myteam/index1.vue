<template>
    <div class="my-team-box">
        <ul>
            <template v-for = '(val, ind) in 5'>
                <li 
                    :key='ind'
                >
                    <span class="team-name">{{val}}soulmate</span>
                    <span 
                        class="team-status"
                        @click='seeFn()'
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
    methods: {
        seeFn () {
            console.log('查看')
            this.$router.push('/user/teamstatus')
        }
    },
    created: function () {
        units.title.set('我的团队');
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
