<template>
  <div>
    <el-container :style="{height:bodyHeight}" id="docBody">
      <el-aside width="200px">
        <el-menu :default-openeds="['1', '2']">
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-menu"></i>图片管理
            </template>
            <el-menu-item index="2-1">图片列表</el-menu-item>
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
          <el-header style="height:130px">
            <el-row>
              <el-col :span="24">
                <div>
                  <el-button size="small" type="info">搜索</el-button>
                  <el-button size="small" type="warning">删除</el-button>
                </div>
              </el-col>
            </el-row>
            <el-row style="padding-top:10px">
              <el-form ref="seachForm" :model="seachForm" label-width="80px">
                <el-col :span="6">
                  <el-form-item label="图片名称">
                    <el-input v-model="seachForm.name"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="图片大小">
                    <el-input v-model="seachForm.size"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="模糊搜索">
                    <el-input v-model="seachForm.like"></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6"></el-col>
              </el-form>
            </el-row>
          </el-header>
          <el-main>
            <div>
              <ul>
                <li class="img-li" v-for="item in imgList" :key="item.src">
                  <el-image
                    style="width: 200px; height: 200px"
                    :src="item.src"
                    :fit="fit"
                    :preview-src-list="srcList"
                  ></el-image>
                </li>
              </ul>
            </div>
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
      seachForm: { name: "", size: "", like: "" },
      img1: "images/j1.jpg",
      img2: "images/j2.jpg",
      fit: "fill",
      srcList: ["images/cai1.jpg", "images/cai2.jpg","images/cai3.jpg","images/j1.jpg","images/j2.jpg" ],
      imgList: [
        { src: "images/cai1.jpg" },
        { src: "images/cai2.jpg" },
        { src: "images/cai3.jpg" },
        { src: "images/j1.jpg" },
        { src: "images/j2.jpg" }
      ]
    };
  },
  mounted() {
    this.bodyHeight = document.documentElement.clientHeight + "px";
  },
  created() {}
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
.img-li {
  border: 1px solid rgb(187, 183, 183);
  width: 200px;
  height: 200px;
  float: left;
  margin-left: 25px;
  list-style: none;
  margin-top: 20px;
}
</style>