<template>
  <div>
    <el-row>
      <el-col :span="24">
        <div>
          <el-button size="small" type="info" @click="getList">搜索</el-button>
          <el-button size="small" type="warning">删除</el-button>
          <el-button size="small" type="success" @click="detail">详情</el-button>
        </div>
      </el-col>
    </el-row>
    <el-row style="padding-top:10px">
      <el-form ref="seachForm" :model="seachForm" label-width="80px">
        <el-col :span="6">
          <el-form-item label="用户名">
            <el-input v-model="seachForm.Name"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="手机号">
            <el-input v-model="seachForm.Mobile"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6"></el-col>
        <el-col :span="6"></el-col>
      </el-form>
    </el-row>
    <div>
      <el-table
        :data="vipList"
        border
        style="width: 100%"
        highlight-current-row
        @current-change="tableCurrentChange"
      >
        <el-table-column type="index" width="50"></el-table-column>
        <el-table-column type="selection" width="50"></el-table-column>
        <el-table-column prop="name" label="姓名"></el-table-column>
        <el-table-column prop="vipno" label="VIPNo"></el-table-column>
        <el-table-column prop="nickName" label="昵称"></el-table-column>
        <el-table-column prop="mobile" label="手机号码"></el-table-column>
        <el-table-column prop="provName" label="省"></el-table-column>
        <el-table-column prop="cityName" label="市"></el-table-column>
      </el-table>
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
    <el-dialog title="客户详细信息" :visible.sync="dialogFormVisible">
      <el-form :model="formDetail">
        <el-form-item label="名称" :label-width="formLabelWidth">
          <el-input v-model="formDetail.name"></el-input>
        </el-form-item>
        <el-form-item label="手机号码" :label-width="formLabelWidth">
          <el-input v-model="formDetail.mobile"></el-input>
        </el-form-item>
        <el-form-item label="生日日期" :label-width="formLabelWidth">
          <el-input v-model="formDetail.birthDay"></el-input>
        </el-form-item>
        <el-form-item label="职业" :label-width="formLabelWidth">
          <el-input v-model="formDetail.cusProfession"></el-input>
        </el-form-item>
        <el-form-item label="QQ号码" :label-width="formLabelWidth">
          <el-input v-model="formDetail.cus_QQ"></el-input>
        </el-form-item>
        <el-form-item label="邮箱号" :label-width="formLabelWidth">
          <el-input v-model="formDetail.cusEmail"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
import axios from "axios";
import moment from 'moment';
export default {
  data() {
    return {
      title: "VIP客户管理",
      seachForm: { Name: "", Mobile: "", PageIndex:1},
      currentPage: 1,
      pageSize: 10,
      totalCount: 1,
      vipList: [],
      dialogFormVisible: false,
      formLabelWidth: "120px",
      formDetail: {
        name: "",
        mobile: "",
        birthDay: "",
        cusProfession: "",
        cus_QQ: "",
        cusEmail: ""
      },
      selectRow: null
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
      var loading = this.$loading({
        lock: true,
        text: "拼命加载中",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)"
      });
      axios
        .post(
          "http://localhost:59371/api/MemberData/GetVipCusList",
          self.seachForm
        )
        .then(function(res) {
          self.vipList = res.data.vipList;
          self.totalCount = res.data.count;
          loading.close();
        });
    },
    handleSizeChange() {},
    handleCurrentChange(val) {
      this.seachForm.PageIndex = val;
      this.getList();
    },
    tableCurrentChange(val) {
      this.selectRow = val;
    },
    detail() {
      var self = this;
      if (self.selectRow != null) {
        var loading = this.$loading({
          lock: true,
          text: "拼命加载中",
          spinner: "el-icon-loading",
          background: "rgba(0, 0, 0, 0.7)"
        });
        axios
          .get(
            "http://localhost:59371/api/MemberData/GetVipCusDetail?vipNo=" +
              self.selectRow.vipno
          )
          .then(function(res) {
            self.dialogFormVisible=true;
            self.formDetail = res.data.model;
            self.formDetail.birthDay=moment(res.data.model.birthDay).format('YYYY-MM-DD')
            loading.close();
          });
      } else {
          this.$message({
          message: '请选择一条数据',
          type: 'warning'
        });
      }
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
body {
  overflow: "hidden";
}
</style>