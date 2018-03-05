<template>
    <div class="dia-box">
        <div class="alert-box">
            您已分配成功
        </div>
    </div>
</template>

<script>
export default {
    name: 'dialogBox'
}
</script>

<style lang='scss'>
    .dia-box{
        position: fixed;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background: rgba(0, 0, 0, 0.5);
        z-index: 1000;
        .alert-box{
            background: #fff;
            position: absolute;
            top: 0;
            bottom: 0;
            right: 0;
            left: 0;
            margin: auto;
            width: 8rem;
            height: 2.5rem;
            border-radius: .1rem;
            text-align: center;
            line-height: 2.5rem;
            font-size: .4rem;
        }
    }
</style>
