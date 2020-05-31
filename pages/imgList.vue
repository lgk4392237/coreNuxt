<template>
  <div>
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
  </div>
</template>
<script>
export default {
  data() {
    return {
      seachForm: { name: "", size: "", like: "" },
      img1: "images/j1.jpg",
      img2: "images/j2.jpg",
      fit: "fill",
      srcList: [
        "images/cai1.jpg",
        "images/cai2.jpg",
        "images/cai3.jpg",
        "images/j1.jpg",
        "images/j2.jpg"
      ],
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