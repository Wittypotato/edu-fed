<template>
  <div class="header">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>活动管理</el-breadcrumb-item>
      <el-breadcrumb-item>活动列表</el-breadcrumb-item>
      <el-breadcrumb-item>活动详情</el-breadcrumb-item>
  </el-breadcrumb>
  <el-dropdown>
    <span class="el-dropdown-link">
      <el-avatar
      shape="square"
      :size="30"
      :src="userInfo.portrait || require('@/assets.default-avatar.png')"
      ></el-avatar>
      <i class="el-icon-arrow-down el-icon--right"></i>
    </span>
    <el-dropdown-menu slot="dropdown">
      <el-dropdown-item>{{userInfo.userName}}</el-dropdown-item>
      <el-dropdown-item 
      disabled
      @click.native="handleLogout"
      >退出</el-dropdown-item>
    </el-dropdown-menu>
  </el-dropdown>
  </div>
</template>

<script>
import vue from 'vue'
import { getUserInfo } from '@/services/user'
export default {
  data() {
    return {
      userInfo: {}
    }
  },
  created () {
    this.loadUserInfo()
  },
  methods: {
    async loadUserInfo () {
      const { data } = await getUserInfo()
      this.userInfo = data.content
    },
    handleLogout() {
      // 清除登录信息
      this.$store.commit('setUser', null)
      // 页面跳转到登录页面
      this.$router.push({
        name: 'login'
      })
    }
  }
}
</script>

<style lang='scss' scoped>
.header{
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  .el-dropdown-link{
    display: flex;
    align-items: center;
  }
}
</style>
