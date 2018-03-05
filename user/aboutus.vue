<!--页面css样式-->
<style scoped>
    .without {
        padding: 23% 36% 7%;
        text-align: center;
    }

    .without img {
        width: 100%;
    }

    .without .p1 {
        font-size: 0.5rem;
        color: #1e1e1e;
        margin-top: 0.5rem;
    }

    .without .p2 {
        font-size: 0.4rem;
        margin-top: 0.1rem;
    }

    .in_list {
        border-bottom: 1px solid #f1f1f1;
        margin-top: 0.3rem;
        margin: 0.5rem;
    }

    .in_list li {
        height: 1.49rem;
        border-bottom: 1px solid #f1f1f1;
        overflow: hidden;
        padding-left: 0.4rem;
        background: #fff;
        margin-top: 0.3rem;
    }

    .in_list li a {
        display: block;
        position: relative;
        padding-right: 0.47rem;
        height: 1.49rem;
        /*line-height: 1.49rem;*/
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
        width: 60%;
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
        /*margin-top: 0.05rem;*/
        -webkit-tap-highlight-color: transparent;
        /* font-family: "微软雅黑"; */
        /* font-family: 'Droidsansfallback'; */
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
        /*line-height: 0rem;*/
        text-align: right;
    }

    .in_list li a .arrow_right {
        position: relative;
        display: block;
        width: 0.5rem;
        height: 1.48rem;
        background: url(../../../src/assets/img/right.png) no-repeat;
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

    ::-webkit-input-placeholder { /* WebKit browsers */
        color: #1e1e1e;
    }

    :-moz-placeholder { /* Mozilla Firefox 4 to 18 */
        color: #1e1e1e;
    }

    ::-moz-placeholder { /* Mozilla Firefox 19+ */
        color: #1e1e1e;
    }

    :-ms-input-placeholder { /* Internet Explorer 10+ */
        color: #fff;
    }
  .company{
    color: #0c80fe;
    font-size: 0.38rem;
    position: absolute;
    bottom: 3%;
    left: 35%;
  }
</style>
<!--关于我们-->
<template>
    <div class="aboutus">
        <div class="without">
            <img src="../../../src/assets/img/wuwei.png">
            <p class="p1">无维</p>
            <p class="p2">版本 1.1.1 Build 1</p>
        </div>
        <div class="in_list">
            <ul>
                <li>
                    <a>
                        <label>我们的邮箱</label>
                        <span class="arrow_right_2"></span>
                        <span class="message">
                          <input type="text" class="text" placeholder="wuwei@wuwei.com" readonly>
                        </span>
                    </a>
                </li>
                <li v-if="false">
                    <a>
                        <label>我们的电话</label>
                        <span class="arrow_right"></span>
                        <span class="message">
                          <input type="text" class="text" placeholder="010-888888" readonly>
                        </span>
                    </a>
                </li>
                <li>
                    <a>
                        <label>我们的微信</label>
                        <span class="arrow_right"></span>
                        <span class="message">
              <input type="text" class="text" placeholder="wuwei888" readonly>
            </span>
                    </a>
                </li>
            </ul>
        </div>
      <div class="company">北京无维科技有限公司</div>
    </div>
</template>
