<template>
  <div class="layout-contaniner">
    <router-view/>
    <van-tabbar v-model="active" router>
      <van-tabbar-item icon="home-o" to="/">首页</van-tabbar-item>
      <van-tabbar-item icon="comment-o" to="/qa">问答</van-tabbar-item>
      <van-tabbar-item icon="video-o" to="/video">视频</van-tabbar-item>
      <van-tabbar-item icon="manager-o" to="/ma">我的</van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  name: 'layoutIndex',
  data() {
    return {
      active: 0
    }
  }
}

</script>
<style lang="less"></style>
