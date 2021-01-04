<template>
  <el-container class="home-container">
    <!--头部布局-->
    <el-header>
      <div>
        <img src="../assets/logo2.png" alt class="logo_img" />
      </div>
      <el-button icon="el-icon-switch-button"  @click="logout">安全退出</el-button>
    </el-header>
    <el-container style="border: 1px solid #eee">
      <!--侧边布局-->
      <el-aside width='200px'>
        <!--伸缩按钮-->
        <div class="toggle-button" @click="toggleCollapase">|||</div>
        <!--侧边栏菜单区 unique-opened="true" 只保持一个菜单展开 router开启路由 active-text-color 颜色-->
        <el-menu @open="handleOpen" @close="handleClose" :default-openeds="['1']" background-color="#303133" text-color="#ffffff" active-text-color="#ffffff" :router="true">
          <el-submenu index="1">
              <template slot="title" ><i class="el-icon-cpu" style="margin-right:7px"></i>主机信息</template>
            <el-menu-item index="Netinfo"><i class="el-icon-monitor" style="margin-right:7px"></i>网络信息</el-menu-item>
            <el-menu-item index="About"><i class="el-icon-info" style="margin-right:7px"></i>关于</el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <!--主体布局-->
      <el-main style="background-color: #ffffff">

          <!--路由占位符-->
          <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>
<script>
export default {
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    logout() {
      window.sessionStorage.clear();
      this.$router.push("/login");
    },
    // 获取所有的导航菜单
  }
};
</script>
<style lang="less" scoped>
.el-header {
  background-color: #66ccff;
  display: flex;
  justify-content: space-between;// 左右贴边
  padding-left: 0%;// 左边界
  align-items: center;// 水平
  color: #fff;
  font-size: 20px;
  > div { //左侧div加布局
    display: flex;
    align-items: center;
    span {
      margin-left: 15px;
    }
  }
}
.el-aside {
  background-color: #303133;
  .el-menu{
    border-right: none;// 对其右边框
  }
}
.el-main {
  background-color: #eaedf1;
}
.home-container {
  height: 100%;
}
.logo_img {
  width: 100%;
  height: 100%;
}
.iconfont{
  margin-right: 10px;
}
.toggle-button{
  background-color:#409eff;
  font-size: 10px;
  line-height: 24px;
  color:#fff;
  text-align: center;
  letter-spacing: 0.2em;
  cursor: pointer;// 显示鼠标指针为：小手
}
</style>