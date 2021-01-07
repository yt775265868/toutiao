<template>
  <div class="login-contaniner">
    <van-nav-bar
      class="app-nav-bar"
      title="登录 / 注册"
      left-arrow
      @click-left="$router.back()"
    />
    <van-form @submit="onLogin">
      <van-field
        v-model="user.mobile"
        icon-prefix="iconfont iconshouji"
        left-icon="iconshouji"
        placeholder="请输入手机号"
        :rules="fromRules.mobile"
      />
      <van-field
        class="send-icon"
        v-model="user.code"
        clearable
        icon-prefix="iconfont iconyanzhengma"
        left-icon="iconyanzhengma"
        placeholder="请输入验证码"
        :rules="fromRules.code">
        <template #button>
          <van-button class="send-btn" size="small" round>发送验证码</van-button>
        </template>
      </van-field>
      <div class="login-btn-wrap">
        <van-button class="login-btn" type="info" block>登陆</van-button>
      </div>      
    </van-form>
  </div>
</template>

<script>
import { login } from '@/api/user'
import { Toast } from 'vant'

export default {
  name: 'loginIndex',
  data() {
    return {
      user: {
        mobile: '',
        code: ''
      },
      fromRules: {
        mobile: [
          { required: true, message: '请填写手机号' },
          { pattern: /^1[3456789]\d{9}$/, message: '手机号格式错误' }
        ],
        code: [
          { required: true, message: '请填写验证码' },
          { pattern: /^\d{6}$/, message: '验证码格式错误' }
        ]
      }
    }  
  },
  methods: {
    async onLogin () {
      Toast.loading({
        message: '登录中...',
        forbidClick: true,
        duration: 0
      })
      try {
        const res = await login(this.user)
        Toast.success('登录成功')
      } catch (err) {
        Toast.fail('登录失败')
      }    
    }
  }
}

</script>
<style lang="less">
.login-contaniner {
  .van-cell {
    align-items: center;
  }
  .send-btn {
    background-color: #ededed;
    .van-button__text {
      font-size: 11px;
      color: #666666;
    }
  }
  .login-btn-wrap {
    padding: 26px 16px;
    .login-btn {
      background-color: #6db4fb;
      border: none;
      .van-button__test {
        font-size: 15px;
      }
    }
}
}
</style>
