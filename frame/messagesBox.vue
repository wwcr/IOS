<template>
    <div class="message-page">
        <div class="msg-box">
            <div class="msg-content">
                010-84685465
            </div>
            <div class="btn-box">
                <div class="button" @click="cancelTel(0)">取消</div>
                <div class="button" @click="cancelTel(1)">呼叫</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        cancelTel (val) {
            this.$emit('cancelTel', val)
        }
    }
}
</script>

<style scoped lang='scss'>
    .message-page{
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, .5);
        font-size: .45rem;
        z-index: 9999;
        .msg-box{
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;
            background: #fff;
            width: 8rem;
            height: 3rem;
            border-radius: .2rem;
            .msg-content{
                text-align: center;
                line-height: 1.8rem;
            }   
            .btn-box{
                position: absolute;
                bottom: 0;
                display: flex;
                width: 100%;
                height: 1.2rem;
                line-height: 1.2rem;
                text-align: center;
                border-top: .03rem solid #f4f4f4;
                .button{
                    flex:1;
                    border: 0;
                    outline: none;
                    background: #fff;
                    &:nth-child(1) {
                        border-right: .03rem solid #f4f4f4;
                        border-bottom-left-radius: .2rem;
                    }
                    &:nth-child(2) {
                        border-bottom-right-radius: .2rem;
                    }
                }
            }
        }
    }
</style>
