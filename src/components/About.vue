<template>
  <div class="hello">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">主机信息</el-breadcrumb-item>
      <el-breadcrumb-item>关于</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card style="height: 700px">
      <i class="el-icon-info"></i>长沙理工大学 刘馨元 版权所有 201819040617 网络1802班
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
