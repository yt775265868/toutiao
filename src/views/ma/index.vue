<template>
  <div class="my-contaniner">
    <van-cell-group v-if="user" class="my-info">
      <van-cell center class="base-info" :border="false">
        <van-image
          class="avatar"
          slot="icon"
          round
          fit="cover"
          :src="currentUser.photo" />
          <div class="name" slot="title">{{ currentUser.name }}</div>
          <van-button class="update-btn" size="small" round>编辑资料</van-button>
      </van-cell>
      <van-grid class="data-info" :border="false">
        <van-grid-item class="data-info-item">
          <div class="text-wrap" slot="text">
            <div class="count">{{ currentUser.art_count}}</div>
            <div class="text">头条</div>
          </div>
        </van-grid-item>
        <van-grid-item class="data-info-item">
          <div class="text-wrap" slot="text">
            <div class="count">{{ currentUser.follow_count}}</div>
            <div class="text">关注</div>
          </div> 
        </van-grid-item>         
        <van-grid-item class="data-info-item">
          <div class="text-wrap" slot="text">
            <div class="count">{{ currentUser.fans_count}}</div>
            <div class="text">粉丝</div>
          </div>          
        </van-grid-item>
        <van-grid-item class="data-info-item">
          <div class="text-wrap" slot="text">
            <div class="count">{{ currentUser.like_count}}</div>
            <div class="text">获赞</div>
          </div>
        </van-grid-item>
      </van-grid>
    </van-cell-group>
    <div v-else class="not-login">
      <div @click="$router.push('/login')">
        <img class="mobile" src="./phone.jpg">
      </div>
      <div class="text">登录 / 注册</div>
    </div>
    <van-grid class="nav-grid" :column-num="2">
      <van-grid-item class="nav-grid-item mb-4" text="收藏" icon-prefix="iconfont iconshoucang" icon="iconshoucang" />
      <van-grid-item class="nav-grid-item" text="历史" icon-prefix="iconfont iconlishi" icon="iconlishi" />
    </van-grid>
    <van-cell title="消息通知" is-link to="/" />
    <van-cell class="mb-4" title="小智通信" is-link to="/" />
    <van-cell v-if="user" class="logout-cell" title="退出登录" @click="onLogout" />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { getCurrentUser } from '@/api/user'
export default {
  name: 'MyIndex',
  data () {
    return {
      currentUser: {}
    }
  },
  created () {
    this.loadCurrentUser()
  },
  computed: {
    ...mapState(['user'])
  },
  methods: {
    async loadCurrentUser () {
      const { data } = await getCurrentUser()
      this.currentUser = data.data
    },
    onLogout () {
      this.$dialog.confirm({
        title: '标题',
        message: '弹窗内容',
      })
        .then(() => {
          // on confirm
          this.$store.commit('setUser', null)
        })
        .catch(() => {
          // on cancel
        })
    }
  }
}

</script>
<style lang="less">
.my-contaniner {
  .my-info {
    background: url("./bg_img.jpg") no-repeat;
    background-size: cover;
    .base-info {
      background-color: unset;
      height: 115px;
      box-sizing: border-box;
      padding-top: 38px;
      padding-bottom: 11px;
      .avatar {
        box-sizing: border-box;
        width: 66px;
        height: 66px;
        border: 1px solid #fff;
        margin-right: 11px;
      }
      .name {
        color: #fff;
        font-size: 15px;
      }
      .update-btn {
        height: 16px;
        font-size: 10px;
        color: #666666;
      }
    }
    .data-info {
      .data-info-item {
        height: 65px;
        color: #fff;
        .text-wrap {
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
          .count {
            font-size: 18px;
          }
          .text {
            font-size: 11px;
          }
        }
      }
    }
    /deep/ .van-grid-item__content {
      background-color: unset;
    }
  }
  .nav-grid {
    .nav-grid-item {
      height: 70px;
      .iconfont {
        font-size: 22px;
      }
      .iconshoucang {
        color: #eb5253;
      }
      .iconlishi {
        color: #ff9d1d;
      }
      .van-grid-item__text {
        font-size: 14px;
        color: #333333;
      }
    }
  }
  .not-login {
    height: 180px;
    background: url("./bg_img.jpg") no-repeat;
    background-size: cover;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    .mobile {
      width: 66px;
      height: 66px;
      border-radius: 50%;
    }
    .text {
      font-size: 14px;
      color: #fff;
    }
  }
  .logout-cell {
    text-align: center;
    color: #d86262;
  }
  .mb-4 {
    margin-bottom: 4px;
  }
}
</style>