<style scoped>
    .popup {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 100000;
        background: rgba(0, 0, 0, .8);
        text-align: center;
    }

    .fixed-ad-con {
        width: 300px;
        margin: 0 auto;
        position: absolute;
        left: 50%;
        top: 50% !important;
        -webkit-transform: translateY(-50%);
        transform: translateY(-50%);
        margin-left: -150px;
    }

    .fixed-ad-img {
        display: block;
        text-align: center;
        max-width: 300px;
        height: auto;
    }

    .fixed-ad-img img {
        width: 85%;
        display: block;
        margin: 0 auto;
    }

    .fixed-ad-img a.look {
        width: 100%;
        display: block;
    }

    .fixed-ad-img a.goon {
        width: 100%;
        display: block;
        margin-top: 0.3rem;
    }

    .close-fixed-ad {
        position: relative;
        width: 20px;
        height: 20px;
        bottom: 0px;
        z-index: 2;
        left: 50%;
        margin-left: -18px;
        margin-top: 20px;
        cursor: pointer;
        background: url(../../../src/assets/img/xx.png) no-repeat;
        background-size: 87%;
    }

    .point {
        /*height: 75px;*/
        background: #fff;
        width: 85%;
        margin: 0 auto;
        padding: 0.4rem 0;
    }
</style>
<template>
    <div class="popup">
        <div class="fixed-ad-con">
            <slot>
                <div class="fixed-ad-img">
                    <img src="../../assets/img/suss.png">
                    <div class="point">
                        <a class="look"><img src="../../../src/assets/img/chakan.png"></a>
                        <a class="goon"><img src="../../../src/assets/img/jixu.png"></a>
                    </div>
                    <div class="close-fixed-ad"></div>
                </div>
            </slot>
        </div>
    </div>
</template>
