<template>
  <div class="login-warp">
    <div class="login-head"></div>
    <div class="login-form">
      <el-form ref="form"
               :model="form">
        <el-form-item>
          <el-input v-model="form.name"
                    placeholder="手机号"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="form.name"
                    placeholder="验证码"></el-input>
        </el-form-item>
        <el-button>获取验证码</el-button>
        <el-form-item>
          <el-button type="primary"
                     @click="onSubmit">登陆</el-button>
          <!-- <el-button>取消</el-button> -->
        </el-form-item>
      </el-form>
    </div>

  </div>
</template>

<script>
export default {
  name: 'AppLogin',
  data () {
    return {
      form: {
        mobile: '',
        code: ''
      }
    }
  },
  methods: {
    onSubmit () {
      console.log('submit!')
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
}
</style>
