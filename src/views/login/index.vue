/* eslint-disable no-unused-vars */
<template>
  <div class="login-warp">
    <div class="login-form-wrap">
      <div class="login-head">
        <img src="./logo_index.png"
             alt="黑马头条">
      </div>
      <div class="login-form">
        <el-form ref="form"
                 :model="form">
          <el-form-item>
            <el-input v-model="form.mobile"
                      placeholder="手机号"></el-input>
          </el-form-item>
          <el-form-item>
            <el-col :span="12">
              <el-input v-model="form.code"
                        placeholder="验证码"></el-input>
            </el-col>
            <el-col :span="4"
                    :offset="2">
              <el-button @click="handleSendCode">获取验证码</el-button>
            </el-col>

          </el-form-item>
          <!-- <el-button>获取验证码</el-button> -->
          <el-form-item>
            <el-button class="btn-login"
                       type="primary"
                       @click="onSubmit">登陆</el-button>
            <!-- <el-button>取消</el-button> -->
          </el-form-item>
        </el-form>
      </div>

    </div>

  </div>
</template>

<script>
// import axios from 'axios'
import axios from 'axios'
import '@/vendor/gt'

export default {
  name: 'AppLogin',
  data () {
    return {
      form: {
        mobile: '18600362956',
        code: ''
      },
      captchaObj: null // 通过initGeetest 得到的机验验证码对象
    }
  },
  methods: {
    onSubmit () {
      console.log('submit!')
    },
    handleSendCode () {
      const { mobile } = this.form
      if (this.captchaObj) {
        return this.captchaObj.verify()
      }
      axios({
        method: 'GET',
        url: `http://ttapi.research.itcast.cn/mp/v1_0/captchas/${mobile}`
      }).then(res => {
        const data = res.data.data
        window.initGeetest({
          // 以下配置参数来自服务端 SDK
          gt: data.gt,
          challenge: data.challenge,
          offline: !data.success,
          new_captcha: data.new_captcha,
          product: 'bind'
        }, (captchaObj) => {
          this.captchaObj = captchaObj
          // 这里可以调用验证实例 captchaObj 的实例方法
          captchaObj.onReady(function () {
            captchaObj.verify()
          }).onSuccess(function () {
            console.log('验证成功了')
          })
        })
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login-warp {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ccc;
  .login-head {
    display: flex;
    justify-content: center;
    margin-bottom: 30px;
    // box-sizing: border-box;
  }
  .login-form-wrap {
    background-color: #fff;
    padding: 50px;
    border-radius: 5%;
    .btn-login {
      width: 100%;
    }
  }
}
</style>
