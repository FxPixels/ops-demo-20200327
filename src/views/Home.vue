<template>
  <div class="home">
    <navbar></navbar>
    <div class="container">
      <div class="left">
        <sections-frame :title="'接口列表'" class="api-list">
          <Input
            v-model="value"
            size="small"
            placeholder="请输入内容"
            suffix-icon="el-icon-search"
          ></Input>

          <div class="tree-title">
            <p>全部接口</p>

            <p><i class="el-icon-folder-add"></i> 新建分类</p>
          </div>

          <div class="tree">
            <div class="block">
              <div class="tree-component">
                <Tree
                  :data="data"
                  node-key="id"
                  default-expand-all
                  :expand-on-click-node="false"
                >
                  <span class="custom-tree-node" slot-scope="{ node, data }">
                    <span>
                      <i
                        v-if="node.label.indexOf('一') != -1"
                        class="el-icon-folder-opened"
                      ></i>
                      <i v-else class="el-icon-document"></i>
                      {{ node.label }}
                    </span>
                    <span>
                      <Button
                        type="text"
                        size="small"
                        @click="() => append(data)"
                      >
                        <i class="el-icon-edit-outline"></i>
                      </Button>
                      <Button
                        type="text"
                        size="small"
                        @click="() => append(data)"
                      >
                        <i class="el-icon-circle-plus-outline"></i>
                      </Button>
                      <Button
                        type="text"
                        size="small"
                        @click="() => remove(node, data)"
                      >
                        <i class="el-icon-circle-close"></i>
                      </Button>
                    </span>
                  </span>
                </Tree>
              </div>
            </div>
          </div>
        </sections-frame>
      </div>
      <div class="center">
        <sections-frame :title="'接口基本属性'">
          <div class="total">
            <div class="total-chart">
              <Progress
                :width="95"
                :stroke-width="8"
                type="dashboard"
                :percentage="percentage"
                :color="colors"
              ></Progress>
              <div class="total-chart-title">根据A+B+C=Z公式得出评分</div>
            </div>
            <div class="total-deal">
              <p>
                发现
                <span>5</span>
                个安全漏洞
              </p>
              <p>
                您的资产已存在安全隐患，可能被病毒或是黑客入侵主机，请您尽快处理。
              </p>
              <p>
                <Button type="primary" size="small">立即处理</Button>
              </p>
            </div>
            <div class="total-info">
              <div class="total-info-item">
                <div class>
                  <img src="@/assets/images/节点.png" alt />
                </div>
                <div>
                  <p>应用服务</p>
                  <p>5120</p>
                </div>
              </div>

              <div class="total-info-item">
                <div class>
                  <img src="@/assets/images/设备.png" alt />
                </div>
                <div>
                  <p>物理层</p>
                  <p>256</p>
                </div>
              </div>

              <div class="total-info-item">
                <div class>
                  <img src="@/assets/images/设备.png" alt />
                </div>
                <div>
                  <p>存储层</p>
                  <p>1024</p>
                </div>
              </div>

              <div class="total-info-item">
                <div class>
                  <img src="@/assets/images/设备.png" alt />
                </div>
                <div>
                  <p>网络层</p>
                  <p>128</p>
                </div>
              </div>
            </div>
          </div>
        </sections-frame>

        <sections-frame :title="'接口拓扑图'" class="topology-frame">
          <div class="topology">
            <topology></topology>
          </div>

          <div class="topology-tip" slot="title-right">
            <p>
              <Popover
                placement="top"
                title="操作提示"
                trigger="hover"
              >
                <div class="topology-tip-content">
                  <p>1、按住 Shift + 鼠标左键点击可进行多选；
                  </p>

                  <p>2、按住 Ctrl + 鼠标左键拖动可进行框选；</p>

                  <p>3、鼠标滚轮可放大缩小视图。</p>
                </div>
                <div slot="reference">
                  <span>操作提示</span>
                  <i class="el-icon-magic-stick"></i>
                </div>
              </Popover>
            </p>

            <p>
              <span>设置</span>
              <i class="el-icon-setting"></i>
            </p>
          </div>
        </sections-frame>
      </div>
      <div class="right">
        <sections-frame :title="'接口监控'" class="charts-data">
          <div class="title-right" slot="title-right">
            <span>设置</span>
            <i class="el-icon-setting"></i>
          </div>
          <div class="select-charts">
            <radio-group v-model="radio" size="mini">
              <radio-button label="压力状态" name="1"></radio-button>
              <radio-button label="负载情况" name="2"></radio-button>
              <radio-button label="可用率统计" name="3"></radio-button>
              <radio-button label="响应时间统计" name="4"></radio-button>
            </radio-group>
          </div>
          <div class="more-charts">
            <charts></charts>
          </div>
        </sections-frame>
        <sections-frame :title="'接口日志'" class="api-detail">
          <div class="title-right" slot="title-right">
            <span>更多</span>
            <i class="el-icon-arrow-right"></i>
          </div>
          <div class="more-message">
            <div class="list">
              <message-item>
                <div class>
                  admin:
                  每周一更新接口，故先停止接口，按照规定对该接口进行检查，虽然检查不出什么毛病。
                </div>
              </message-item>
              <message-item>
                <div class>
                  admin:
                  每周一更新接口，故先停止接口，按照规定对该接口进行检查，虽然检查不出什么毛病。
                </div>
              </message-item>
              <message-item>
                <div class>
                  admin:
                  每周一更新接口，故先停止接口，按照规定对该接口进行检查，虽然检查不出什么毛病。
                </div>
              </message-item>
              <message-item>
                <div class>
                  admin:
                  每周一更新接口，故先停止接口，按照规定对该接口进行检查，虽然检查不出什么毛病。
                </div>
              </message-item>
            </div>
          </div>
        </sections-frame>
        <sections-frame :showTitle="false" class="share-detail">
          <div>
            <div class="api-operations">
              <Button type="primary" size="mini" disabled>启动</Button>
              <Button type="warning" size="mini">停用</Button>
              <Button type="danger" size="mini" disabled>删除</Button>
            </div>

            <div class="more-operations">
              <dropdown trigger="click">
                <span class="el-dropdown-link">
                  更多操作
                  <i class="el-icon-caret-bottom el-icon--right"></i>
                </span>
                <dropdown-menu slot="dropdown">
                  <dropdown-item class="clearfix mini-text">
                    设置权限
                    <!-- <badge class="mark" :value="12" /> -->
                  </dropdown-item>
                </dropdown-menu>
              </dropdown>
            </div>
          </div>
        </sections-frame>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import {
  Button,
  Input,
  Progress,
  Tree,
  RadioGroup,
  RadioButton,
  DropdownMenu,
  DropdownItem,
  Dropdown,
  Popover
} from "element-ui";
import sectionsFrame from "../components/sections.vue";
import navbar from "../components/navbar.vue";
import messageItem from "../components/message_item.vue";
import charts from "../components/charts.vue";
import topology from "../components/topology.vue";
import $ from "jquery";

let id = 1000;

export default {
  name: "Home",
  components: {
    Button,
    sectionsFrame,
    navbar,
    Input,
    Progress,
    Tree,
    RadioGroup,
    RadioButton,
    DropdownMenu,
    DropdownItem,
    Dropdown,
    messageItem,
    charts,
    topology,
    Popover
  },
  data() {
    const data = [
      {
        id: 1,
        label: "一级 1",
        children: [
          {
            id: 4,
            label: "二级 1-1",
            children: [
              {
                id: 9,
                label: "三级 1-1-1"
              },
              {
                id: 10,
                label: "三级 1-1-2"
              }
            ]
          }
        ]
      },
      {
        id: 2,
        label: "一级 2",
        children: [
          {
            id: 5,
            label: "二级 2-1"
          },
          {
            id: 6,
            label: "二级 2-2"
          }
        ]
      },
      {
        id: 3,
        label: "一级 3",
        children: [
          {
            id: 7,
            label: "二级 3-1"
          },
          {
            id: 8,
            label: "二级 3-2"
          }
        ]
      },
      {
        id: 11,
        label: "一级 4",
        children: [
          {
            id: 12,
            label: "二级 4-1"
          },
          {
            id: 13,
            label: "二级 4-2"
          }
        ]
      }
    ];

    return {
      value: "",
      data: JSON.parse(JSON.stringify(data)),
      radio: "压力状态",
      percentage: 75,
      colors: [
        { color: "#37A6E7", percentage: 20 },
        { color: "#1989fa", percentage: 80 },
        { color: "#6f7ad3", percentage: 100 }
      ]
    };
  },
  mounted() {
    let el = $(".el-progress__text");
    el.html(`
      <div>
        <p style="color: #37A6E7">${this.percentage}</p>
        <p>系统评分</p>
      </div>
    `);
  },
  methods: {
    append(data) {
      const newChild = { id: id++, label: "testtest", children: [] };
      if (!data.children) {
        this.$set(data, "children", []);
      }
      data.children.push(newChild);
    },

    remove(node, data) {
      const parent = node.parent;
      const children = parent.data.children || parent.data;
      const index = children.findIndex(d => d.id === data.id);
      children.splice(index, 1);
    }
  }
};
</script>

<style lang="less">
.home {
  .el-progress__text {
    p:first-child {
      font-size: 30px !important;
      font-weight: bold;
    }

    p:last-child {
      margin-top: 8px;
    }
  }

  .el-radio-group {
    .el-radio-button {
      .el-radio-button__inner {
        border: 0 !important;
      }
    }
    .is-active {
      .el-radio-button__inner {
        border-radius: 4px !important;
      }
    }
  }

  .left {
    .api-list {
      height: 100%;

      .sections-content {
        height: calc(100% - 30px);
      }
    }
  }

  .center {
    .topology-frame {
      .sections-content {
        height: calc(100% - 15px * 2);
      }
    }

    .topology {
      .minimap {
        position: absolute;
        left: 0;
        top: 10px;
        border: 1px solid rgba(55, 166, 231, 0.5);
      }

      .g6-tooltip {
        padding: 8px;
        color: #444;
        box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
        border-radius: 5px;
        border: 1px solid #ebeef5;
        background-color: rgba(255, 255, 255, 0.8);

        .g6-tooltip-html {
          font-size: 13px;

          & > div {
            margin-bottom: 6px;

            &:first-child {
              span {
                font-weight: bold;
              }
            }

            &:last-child {
              margin-bottom: 0;
            }
          }
        }
      }
    }
  }

  .right {
    .charts-data {
      min-height: 280px;
    }

    .api-detail {
      // display: flex;
      // flex-direction: column;
      height: 100%;
      // max-height: 260px;
      // overflow: auto;

      .sections-content {
        display: flex;
        flex-direction: column;
        height: calc(100% - 30px);
        // overflow: hidden;
        position: relative;
        // top: 15px;
      }
    }

    .el-dropdown-link {
      font-size: 12px;
    }
    .share-detail {
      min-height: 24px;
      .el-button--mini {
        padding: 5px 7px !important;
      }

      .more-operations {
      }
    }
  }
}
.mini-text {
  font-size: 12px !important;
  line-height: 24px !important;
}

.el-popover__title {
  font-size: 14px !important;
}

.topology-tip-content {
  font-size: 12px !important;
}
</style>

<style lang="less" scoped>
.home {
  display: flex;
  flex-direction: column;
  height: 100%;

  .container {
    padding: 15px;
    background-color: #f0f3f5;
    flex: 1;
    display: flex;

    & > div {
      margin-right: 15px;
      height: 100%;
    }

    & > div:last-child {
      margin-right: 0;
    }

    .tree-component,
    .more-message {
      padding-right: 5px;

      &::-webkit-scrollbar {
        /*滚动条整体样式*/
        width: 8px; /*高宽分别对应横竖滚动条的尺寸*/
        height: 1px;
      }
      &::-webkit-scrollbar-thumb {
        /*滚动条里面小方块*/
        border-radius: 10px;
        // box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
        background: #c1c1c1;
      }
      &::-webkit-scrollbar-track {
        /*滚动条里面轨道*/
        // box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
        border-radius: 10px;
        background: #ededed;
      }
    }

    .left {
      width: 20%;
      min-width: 258px;
      display: flex;
      flex-direction: column;

      .sections {
        flex: 1;
        margin-bottom: 0;
      }

      .tree-title {
        padding-top: 15px;
        padding-bottom: 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        p:first-child {
          font-size: 14px;
          font-weight: bold;
        }

        p:last-child {
          font-size: 12px;
          cursor: pointer;
          color: #37a6e7;
        }
      }

      .tree {
        height: calc(100% - 78px);
        position: relative;

        .block {
          display: flex;
          flex-direction: column;
          height: 100%;
        }

        .tree-component {
          flex-grow: 1;
          height: 0;
          overflow-y: auto;
        }

        .custom-tree-node {
          flex: 1;
          display: flex;
          align-items: center;
          justify-content: space-between;
          font-size: 14px;
          // padding-right: 8px;

          i {
            font-size: 13px;
          }
        }
      }
    }

    .center {
      // width: 60%;
      width: 750px;
      flex-shrink: 0;
      display: flex;
      flex-direction: column;

      .total {
        display: flex;

        .total-chart {
          width: auto;
          padding: 15px;
          padding-bottom: 0;
          margin-right: 20px;
          text-align: center;

          .total-chart-title {
            text-align: center;
            font-size: 12px;
            padding-bottom: 15px;
            // color: ;
          }
        }

        .total-deal {
          width: 200px;
          display: flex;
          flex-direction: column;
          justify-content: center;
          // margin-right: 30px;

          & > p {
            margin-bottom: 10px;
          }

          & > p:first-child {
            span {
              color: #2598e6;
              font-weight: bold;
            }
          }

          & > p:nth-child(2) {
            font-size: 13px;
            text-align: justify;
          }
        }

        .total-info {
          flex: 1;
          display: flex;
          flex-wrap: wrap;
          justify-content: flex-end;

          .total-info-item {
            display: flex;
            align-items: center;
            flex-shrink: 0;
            margin-right: 20px;
            min-width: 120px;
            // margin-top: 10px;

            & > div:first-child {
              margin-right: 10px;
              display: flex;
              align-items: center;

              img {
                width: 40px;
              }
            }

            & > div:last-child {
              p:first-child {
                font-size: 14px;
              }
              p:last-child {
                font-size: 20px;
                color: #2598e6;
                font-weight: bold;
              }
            }
          }

          .total-info-item:nth-child(2n) {
            margin-right: 0;
          }
        }
      }

      .topology-frame {
        flex: 1;
        margin-bottom: 0;

        .sections-content {
          height: 100%;
        }
      }

      .topology {
        position: relative;
        height: 100%;
      }

      .topology-tip {
        // position: absolute;
        // bottom: 3px;
        // right: 0;
        font-size: 13px;
        font-weight: normal;
        color: #3092cb;
        display: flex;
        line-height: 0;

        & > p {
          margin-left: 15px;
          cursor: pointer;

          span {
            padding-right: 5px;
          }
        }
      }
    }

    .right {
      flex: 1;
      display: flex;
      flex-direction: column;

      .title-right {
        color: #37a6e7;
        cursor: pointer;
        font-size: 13px;
        font-weight: normal;

        span {
          padding-right: 3px;
        }
      }

      .select-charts {
        margin-top: 10px;
        margin-bottom: 20px;
      }

      .api-detail {
        height: 100%;
      }

      .more-message {
        flex-grow: 1;
        height: 0;
        overflow-y: auto;

        .list {
          text-align: justify;
        }
      }

      .list {
        overflow-y: auto;
      }

      .share-detail {
        margin-bottom: 0;

        div {
          display: flex;
          justify-content: space-between;
          align-items: center;
        }

        .more-operations {
          cursor: pointer;
        }
      }
    }
  }
}
</style>
