<template>
  <div>
    <!-- 上传图片按钮 -->
    <el-upload
        class="upload-demo"
        action="/uploadUrl"
        :show-file-list="false"
        :on-success="handleUploadSuccess"
        :before-upload="beforeUpload"
    >
      <el-button size="small" type="primary">点击上传图片</el-button>
    </el-upload>

    <!-- 显示上传的图片 -->
    <div v-if="imageUrl" class="image-container">
      <img :src="imageUrl" alt="Uploaded Image" class="uploaded-image" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageUrl: '', // 保存上传的图片地址
    };
  },
  methods: {
    // 在上传之前的钩子函数，可用于限制文件大小、文件类型等
    beforeUpload(file) {
      const isJPG = file.type === 'image/jpeg';
      const isPNG = file.type === 'image/png';
      const isLt2M = file.size / 1024 / 1024 < 2; // 限制图片大小小于2MB

      if (!isJPG && !isPNG) {
        this.$message.error('上传图片只能是 JPG/PNG 格式!');
        return false;
      }
      if (!isLt2M) {
        this.$message.error('上传图片大小不能超过 2MB!');
        return false;
      }
      return true;
    },
    // 上传成功的回调函数
    handleUploadSuccess(response, file) {
      this.imageUrl = URL.createObjectURL(file.raw); // 获取上传成功后的图片地址
    },
  },
};
</script>

<style scoped>
.upload-demo {
  margin-bottom: 20px;
}
.uploaded-image {
  max-width: 100%;
  max-height: 300px;
}
</style>
