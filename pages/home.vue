<template>
  <div>
    <el-container :style="{height:bodyHeight}" id="docBody">
      <el-aside width="200px">
        <el-menu :default-openeds="['1', '2']">
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-menu"></i>图片管理
            </template>
            <el-menu-item index="2-1">
               <el-link :underline="false" @click="goMain('/imgList')">图片列表</el-link>
            </el-menu-item>
            <el-menu-item index="2-2">图片上传</el-menu-item>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-setting"></i>个人管理
            </template>
            <el-menu-item index="3-1">帐户管理</el-menu-item>
            <el-menu-item index="3-2">信息设置</el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>

      <el-container>
        <el-container>
          <el-main>
            <iframe scrolling="no" width="100%" height="100%" border="0" :src="mainSrc" frameborder=”no”></iframe>
          </el-main>
        </el-container>
      </el-container>
    </el-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      bodyHeight: "",
      mainSrc:''
    };
  },
   mounted() {
    this.bodyHeight = document.documentElement.clientHeight + "px";
  },
  methods:{
    goMain(src){
      this.mainSrc=src;
    }
  }
};
</script>
<style scoped>
.el-header,
.el-footer {
  color: #333;
  text-align: left;
  line-height: 60px;
}

.el-aside {
  color: #333;
  text-align: center;
}

.el-main {
  color: #333;
}

</style>