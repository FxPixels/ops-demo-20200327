<template>
  <div class="message-item">
    <div class="title">
      <p class="name">{{name}}</p>
      <p class="time">{{time}}</p>
    </div>
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    name: {
      type: String,
      default: "接口操作名"
    },
    time: {
      type: String,
      default: "2020-02-02 02:02:02"
    }
  }
};
</script>

<style lang="less" scoped>
.message-item {
  padding: 5px;
  margin-bottom: 10px;
}

.title {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
  align-items: center;

  & > p {
    font-size: 13px;

    &:last-child {
      color: #999999;
    }
  }

  .time{
    font-size: 12px;
  }
}

.content{
   font-size: 12px;
}
</style>