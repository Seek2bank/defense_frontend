<script>
import axios from "axios";
import {navy as response} from "mockjs";

export default {
  data(){
    return{
      searchInfoTeacher: ''
    }
  },
  methods: {
    goHome() {
      this.$router.push('/forum').catch(error => {
        if (error.name != 'NavigationDuplicated') {
          throw error;
        };}); // 假设使用 Vue Router 进行跳转
      console.log('Menu item clicked');
    },
    goActPost() {
      this.$router.push('/post').catch(error => {
        if (error.name != 'NavigationDuplicated') {
          throw error;
        };}); // 假设使用 Vue Router 进行跳转
      console.log('Menu item clicked');
    },
    goValuePost() {
      this.$router.push('/post/value').catch(error => {
        if (error.name != 'NavigationDuplicated') {
          throw error;
        };});  // 假设使用 Vue Router 进行跳转
      console.log('Menu item clicked');
    },
    goMyPost() {
      this.$router.push('/post/pub').catch(error => {
        if (error.name != 'NavigationDuplicated') {
          throw error;
        };}); // 假设使用 Vue Router 进行跳转
      console.log('Menu item clicked');
    },
    goAi(){
      this.$router.push('/forum/ai'); // 假设使用 Vue Router 进行跳转
      console.log('Menu item clicked');
    },
    submitName() {
      try {
        const result = axios.post('http://localhost:8080/api/getInfo', {
          name: this.searchInfoTeacher
        });
        response.value = result.data; // 和后端统一
      } catch (error) {
        console.error('Error submitting name:', error);
        response.value = 'Error submitting name';
      }
    },
  }
}

</script>

<template>
  <el-menu
      :default-active="activeIndex2"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
      background-color="#112e4d"
      text-color="#fff"
      active-text-color="#ffd04b"
  >
    <el-menu-item index="1" @click="goHome">消息中心</el-menu-item>
    <el-submenu index="2">
      <template slot="title">我的论坛</template>
      <el-menu-item index="2-1" @click="goActPost">我赞/踩过的帖子</el-menu-item>
      <el-menu-item index="2-2" @click="goValuePost">我收藏的帖子</el-menu-item>
      <el-menu-item index="2-3" @click="goMyPost">我发表的帖子</el-menu-item>
    </el-submenu>
    <el-menu-item index="4" @click="goAi">论坛智能助手</el-menu-item>
    <el-menu-item class="reply-item">
      <el-menu-item style="display: flex; align-items: center;">
        <el-input v-model="searchInfoTeacher" style="margin-right: 10px; width: 300px; " placeholder="在这里，一切都是匿名的..."></el-input>
        <el-button style="background-color: #0f2d4b; color: rgb(15,45,75);" type="primary" size="mini" @click="submitName"><i class="el-icon-search" style="color: white;"></i></el-button>
      </el-menu-item>
    </el-menu-item>
  </el-menu>
</template>

<style scoped>

</style>