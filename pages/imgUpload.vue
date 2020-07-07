<template>
  <div>
    <div style="margin-top:15px;padding-bottom:15px;">
      <el-button size="small" type="success" @click="uploadStart">开始上传</el-button>
    </div>
    <el-upload
      action="http://localhost:59371/api/MemberData/UploadFile"
      ref="imgUpload"
      list-type="picture-card"
      multiple
      :on-preview="handlePictureCardPreview"
      :on-remove="handleRemove"
      :auto-upload="false"
    >
      <i class="el-icon-plus"></i>
    </el-upload>
    <el-dialog :visible.sync="dialogVisible">
      <img width="100%" :src="dialogImageUrl" alt />
    </el-dialog>
  </div>
</template>
<script>
export default {
  data() {
    return {
      dialogVisible: false,
      dialogImageUrl: ""
    };
  },
  methods: {
    handlePictureCardPreview(file) {
      this.dialogImageUrl = file.url;
      this.dialogVisible = true;
    },
    handleRemove() {},
    uploadStart(){
         this.$refs.imgUpload.submit();
    }
  }
};
</script>