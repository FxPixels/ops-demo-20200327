<template>
  <div class="sections">
    <div v-if="showTitle" class="sections-title">
      <div>
        <i></i>
        <span>{{ title }}</span>
      </div>
      <div>
        <slot name="title-right"></slot>
      </div>
    </div>
    <div class="sections-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showTitle: {
      type: Boolean,
      default: true
    },
    title: {
      type: String,
      default: "模块标题"
    }
  }
};
</script>

<style lang="less" scoped>
.sections {
  padding: 15px;
  background-color: #fff;
  margin-bottom: 15px;
  transition: 0.3s;
  outline-color: #ebeef5;
  border-radius: 5px;
  // overflow: hidden;
  // outline-radius: 5px;
  // height: 100%;

  &:hover {
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
    outline: 1px solid #ebeef5;
  }

  .sections-title {
    font-size: 15px;
    padding-bottom: 10px;
    display: flex;
    font-weight: bold;
    justify-content: space-between;

    & > div:first-child {
      display: flex;
      align-items: center;
      i {
        width: 3px;
        height: 14px;
        background-color: #3091ca;
        display: inline-block;
        margin-right: 5px;
      }
    }
  }

  // & > div:last-child {
  //   display: flex;
  //   flex: 1;
  //   overflow: auto;
  //   height: 0; //纵向需要滚动条的话
  // }
}
</style>
