<template>
  <div class="page-content">
    <TopBar></TopBar>
    <div style="width: 100%; height: 4rem"></div>
    <div class="pageMain">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import TopBar from '../components/TopBar'
import picture from '@/assets/bk.jpg'

export default {
  data: function () {
    return {
      token: sessionStorage.getItem('token'),
      styles: {
        backgroundImage: `url(${picture})`,
        // background: 'no-repeat'
        backgroundRepeat: 'no-repeat',

        backgroundSize: '100% 100%',
        backgroundAttachment: 'fixed'
      }
    }
  },
  components: {
    TopBar
  },
  beforeCreate() {
    const token = sessionStorage.getItem('token')
    if (!token) {
      this.$router.push({ name: 'login' })
    }
  },
  destroyed() {
    sessionStorage.clear()
  },
  mounted() {
    this.handleMounted()
  },
  methods: {
    handleSignout() {
      // 清除token
      sessionStorage.clear()
      // 提示消息
      this.$message.success('退出成功')
      // 回到登陆页面
      this.$router.push({ name: 'login' })
    },
    handleIndex() {
      this.$router.push({ name: 'index' })
    },
    async handleMounted() {
      //
    }
  }
}

</script>

<style lang='less'>
.page-content {
  // background: #eee;
  width: 100%;
  height: 100%;
}
.pageMain {
  //
}
</style>
