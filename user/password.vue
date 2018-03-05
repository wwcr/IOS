<style scoped>
  .pass h6{
    text-align: center;
    margin-top: 25%;
    font-weight: normal;
    font-size: 0.4rem;
  }
  .list{
    padding: 0 0.5rem;
  }
  .tel{
    margin-top: 5%;
    font-size: 0.38rem;
    line-height: 0.38rem;
    color: #666666;
    border-bottom: 1px solid #f1f1f1;
    height: 1.53rem;
    width: 100%;
  }
  .tel input{
    display: block;
    height: 1.5rem;
    width: 100%;
    line-height: 1.5rem;
    padding-left: 0.5rem;
  }
  .yzm{
    border-bottom: 1px solid #f1f1f1;
    font-size: 0.38rem;
    line-height: 0.38rem;
    color: #666666;
    height: 1.53rem;
    width: 100%;
    background:#fff;
  }
  .yzm input{
    width: 75%;
    height: 1.5rem;
    line-height: 1.5rem;
    padding-left: 0.5rem;
    float: left;
  }
  .yzm a{
    width: 25%;
    height: 1.5rem;
    display: inline-block;
    line-height: 1.5rem;
    color: #2c7dfe;
    font-size: 0.26rem;
  }
  .sub_next {
    padding: 0.58rem 0.75rem 0.63rem;
    background: #fff;
  }
  .sub_next a {
    display: block;
    background: #377bee;
    color: #fff;
    text-align: center;
    line-height: 1.3rem;
    font-size: 0.52rem;
    border-radius: 10px;
  }
  .sub_next a.gray{
    background: #b4b4b4;
  }
</style>
<!--找回密码-->
<template>
  <div class="pass">
      <h6>请输入您的用户名</h6>
      <div class="list">
        <div class="tel">
          <input type="tel" placeholder="请输入正确的手机号"/>
        </div>
        <div class="yzm">
          <input type="text" placeholder="请输入正确的验证码"/>
          <a>获取验证码</a>
        </div>
      </div>
    <div class="sub_next ">
      <a class="gray" @click="submit">下一步</a>
    </div>
  </div>
</template>
