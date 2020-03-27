<template>
  <div class="navbar">
    <div class="left">
      <div class="title">可视化API接口管理平台</div>
    </div>
    <div class="right">
      <div class="user">
        <div class="user-item">
          <i class="el-icon-chat-line-square"></i>
        </div>
        <div class="user-item">
          <i class="el-icon-user"></i>
          <!-- <avatar size="small" icon="el-icon-user-solid"></avatar> -->
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Avatar } from "element-ui";
export default {
  components: {
    Avatar
  }
};
</script>
<style lang="less" scoped>
.navbar {
  padding: 15px;
  background-color: #37a6e7;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 18px;
  color: #fff;

  .title {
    font-weight: bold;
  }

  .user {
    display: flex;

    .user-item {
      margin-left: 10px;
    }
  }
}
</style>
