<template>
  <div>
    <el-row>
      <el-col :span="24">
        <div>
          <el-button size="small" type="info" @click="getList">搜索</el-button>
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
            style="width: 195px; height: 195px"
            :src="item.src"
            :fit="fit"
            :preview-src-list="srcList"
          ></el-image>
        </li>
      </ul>
    </div>
    <div style="clear: both; text-align: right;padding-top:15px;">
      <el-pagination
      background
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="totalCount"
      ></el-pagination>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      title: "图片管理",
      seachForm: { name: "", size: "", like: "" },
      img1: "images/j1.jpg",
      img2: "images/j2.jpg",
      fit: "fill",
      srcList: [],
      imgList: [],
      currentPage:1,
      pageIndex:1,
      pageSize:10,
      totalCount:1
    };
  },
  created() {
    this.getList();
  },
  head() {
    return {
      title: this.title
    };
  },
  methods: {
    getList() {
      var self = this;
      const loading = this.$loading({
          lock: true,
          text: '拼命加载中',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
      axios
        .get("http://localhost:59371/api/MemberData/GetFile?pageIndex="+self.pageIndex)
        .then(function(res) {
          self.srcList=[];
          self.imgList=[];
          var goodList = res.data.fileList;
          self.totalCount=res.data.count;
          for (let i = 0; i < goodList.length; i++) {
            var imgSrc =
              "https://vipauth.kingtaifook.com/Resource/Product/" +
              goodList[i].afnewName;
            self.srcList.push(imgSrc);
            self.imgList.push({ src: imgSrc });
          }
          loading.close();
        });
    },
    handleSizeChange(){
      
    },
    handleCurrentChange(val){
      this.pageIndex=val;
      this.getList();
    }
  }
};
</script>
<style scoped>
.img-li {
  border: 1px solid rgb(226, 226, 226);
  width: 200px;
  height: 200px;
  float: left;
  margin-left: 25px;
  list-style: none;
  margin-top: 20px;
}
.img-li img {
  margin: 0 auto;
 
}
.img-li:hover {
  box-shadow: 0px 0px 2px 3px rgb(235, 232, 232);
}
body{
    overflow:"hidden";  
}
</style>