<template>
  <div class="home">
    <navbar></navbar>
    <div class="container">
      <div class="left">
        <sections-frame :title="'接口列表'" class="api-list">
          <Input v-model="value" size="small" placeholder="请输入内容" suffix-icon="el-icon-search"></Input>

          <div class="tree-title">
            <p>全部接口</p>

            <p>
              <i class="el-icon-folder-add"></i> 新建分类
            </p>
          </div>

          <div class="tree">
            <!-- <Tree
              :data="data"
              show-checkbox
              node-key="id"
              default-expand-all
              :expand-on-click-node="false"
              :render-content="renderContent"
            ></Tree>-->

            <div class="block">
              <div class="tree-component">
                <Tree :data="data" node-key="id" default-expand-all :expand-on-click-node="false">
                  <span class="custom-tree-node" slot-scope="{ node, data }">
                    <span>
                      <i v-if="node.label.indexOf('一') != -1" class="el-icon-folder-opened"></i>
                      <i v-else class="el-icon-document"></i>
                      {{ node.label }}
                    </span>
                    <span>
                      <Button type="text" size="small" @click="() => append(data)">
                        <i class="el-icon-edit-outline"></i>
                      </Button>
                      <Button type="text" size="small" @click="() => append(data)">
                        <i class="el-icon-circle-plus-outline"></i>
                      </Button>
                      <Button type="text" size="small" @click="() => remove(node, data)">
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
                :stroke-width="12"
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
              <p>您的资产已存在安全隐患，可能被病毒或是黑客入侵主机，请您尽快处理。</p>
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
            <div id="mountNode"></div>
            <div class="topology-tip">
              <p>
                <i class="el-icon-warning-outline"></i>
                按住 Shift + 鼠标左键点击可进行多选，按住 Ctrl + 鼠标左键拖动可进行框选，鼠标滚轮可放大缩小视图。
              </p>
            </div>
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
            <div id="c2"></div>
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
                <div class>admin: 每周一更新接口，故先停止接口，按照规定对该接口进行检查，虽然检查不出什么毛病。</div>
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
                    评论
                    <!-- <badge class="mark" :value="12" /> -->
                  </dropdown-item>
                  <dropdown-item class="clearfix mini-text">
                    回复
                    <!-- <badge class="mark" :value="3" /> -->
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
  Dropdown
} from "element-ui";
import sectionsFrame from "../components/sections.vue";
import navbar from "../components/navbar.vue";
import messageItem from "../components/message_item.vue";
import G6, { Minimap } from "@antv/g6";
const Util = G6.Util;
const facility = require("../assets/images/数据库.png"); //设备
import { Chart } from "@antv/g2";
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
    messageItem
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
      radio: "1",
      percentage: 70,
      colors: [
        { color: "#37A6E7", percentage: 20 },
        { color: "#1989fa", percentage: 80 },
        { color: "#6f7ad3", percentage: 100 }
      ],
      g6Data: {
        // 点集
        nodes: [
          {
            id: "node1", // String，该节点存在则必须，节点的唯一标识
            // x: 100, // Number，可选，节点位置的 x 值
            // y: 200, // Number，可选，节点位置的 y 值
            label: "服务器1",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // style: {
            //   fill: "#fff",
            //   fontSize: 12
            // }
          },
          {
            id: "node2", // String，该节点存在则必须，节点的唯一标识
            label: "服务器2",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node3", // String，该节点存在则必须，节点的唯一标识
            label: "服务器3",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node4", // String，该节点存在则必须，节点的唯一标识
            label: "服务器4",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node5", // String，该节点存在则必须，节点的唯一标识
            label: "服务器5",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node6", // String，该节点存在则必须，节点的唯一标识
            label: "服务器6",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node7", // String，该节点存在则必须，节点的唯一标识
            label: "服务器7",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node8", // String，该节点存在则必须，节点的唯一标识
            label: "服务器8",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node9", // String，该节点存在则必须，节点的唯一标识
            label: "服务器9",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node10", // String，该节点存在则必须，节点的唯一标识
            label: "服务器10",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node11", // String，该节点存在则必须，节点的唯一标识
            label: "服务器11",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          },
          {
            id: "node12", // String，该节点存在则必须，节点的唯一标识
            label: "服务器12",
            img: facility,
            type: "myimg",
            size: 70,
            labelCfg: {
              style: {
                fontSize: 14
              }
            }
            // x: 300, // Number，可选，节点位置的 x 值
            // y: 200 // Number，可选，节点位置的 y 值
          }
        ],
        // 边集
        edges: [
          {
            source: "node1", // String，必须，起始点 id
            target: "node2", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接1",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          },
          {
            source: "node3", // String，必须，起始点 id
            target: "node4", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接2",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          },
          {
            source: "node3", // String，必须，起始点 id
            target: "node5", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接3",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          },
          {
            source: "node5", // String，必须，起始点 id
            target: "node6", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接3",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          },
          {
            source: "node7", // String，必须，起始点 id
            target: "node8", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接4",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          },
          {
            source: "node9", // String，必须，起始点 id
            target: "node10", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接5",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          },
          {
            source: "node11", // String，必须，起始点 id
            target: "node12", // String，必须，目标点 id
            // style: {
            //   endArrow: true,
            //   // stroke: "RGB(95,99,104)",
            //   lineWidth: 3
            // },
            label: "连接6",
            labelCfg: {
              autoRotate: true,
              refY: 10,
              style: {
                fontSize: 14
              }
            }
          }
        ]
      }
    };
  },
  mounted() {
    this.setChart_2();
    this.setTopology();

    let minimapEl = $(".minimap");
    minimapEl.append(`
      <p class="mini-text" style="text-align:center">缩略图</p>
    `);

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
    },

    renderContent(h, { node, data, store }) {
      return (
        <span class="custom-tree-node">
          <span>{node.label}</span>
          <span>
            <el-button
              size="mini"
              type="text"
              on-click={() => this.append(data)}
            >
              Append
            </el-button>
            <el-button
              size="mini"
              type="text"
              on-click={() => this.remove(node, data)}
            >
              Delete
            </el-button>
          </span>
        </span>
      );
    },
    setChart_2() {
      const data = [
        { country: "Asia", year: "1750", value: 502 },
        { country: "Asia", year: "1800", value: 635 },
        { country: "Asia", year: "1850", value: 809 },
        { country: "Asia", year: "1900", value: 5268 },
        { country: "Asia", year: "1950", value: 4400 },
        { country: "Asia", year: "1999", value: 3634 },
        { country: "Asia", year: "2050", value: 947 },
        { country: "Africa", year: "1750", value: 106 },
        { country: "Africa", year: "1800", value: 107 },
        { country: "Africa", year: "1850", value: 111 },
        { country: "Africa", year: "1900", value: 1766 },
        { country: "Africa", year: "1950", value: 221 },
        { country: "Africa", year: "1999", value: 767 },
        { country: "Africa", year: "2050", value: 133 },
        { country: "Europe", year: "1750", value: 163 },
        { country: "Europe", year: "1800", value: 203 },
        { country: "Europe", year: "1850", value: 276 },
        { country: "Europe", year: "1900", value: 628 },
        { country: "Europe", year: "1950", value: 547 },
        { country: "Europe", year: "1999", value: 729 },
        { country: "Europe", year: "2050", value: 408 },
        { country: "Oceania", year: "1750", value: 200 },
        { country: "Oceania", year: "1800", value: 200 },
        { country: "Oceania", year: "1850", value: 200 },
        { country: "Oceania", year: "1900", value: 460 },
        { country: "Oceania", year: "1950", value: 230 },
        { country: "Oceania", year: "1999", value: 300 },
        { country: "Oceania", year: "2050", value: 300 }
      ];
      const chart = new Chart({
        container: "c2",
        autoFit: true,
        height: 160
      });

      chart.data(data);
      chart.scale("year", {
        type: "linear",
        tickInterval: 50
      });
      chart.scale("value", {
        nice: true
      });

      chart.tooltip({
        showCrosshairs: true,
        shared: true
      });

      chart
        .area()
        .adjust("stack")
        .position("year*value")
        .color("country");
      chart
        .line()
        .adjust("stack")
        .position("year*value")
        .color("country");

      chart.interaction("element-highlight");

      chart.render();
    },
    setTopology() {
      G6.registerNode(
        "myimg",
        {
          afterDraw(cfg, group) {
            // console.log(cfg);
            const width = cfg.size + 3;
            const height = cfg.size + 6;
            const x = -cfg.size / 2 - 1;
            const y = -cfg.size / 2 - 3;
            // console.log('x',x)
            const rect = group.addShape("rect", {
              attrs: {
                x: x,
                y: y,
                width: width,
                height: height,
                radius: 5,
                cursor: "pointer",
                // strokeOpacity: 0,
                stroke: "RGBA(255,255,255,0)"
              }
            });
          },
          setState(name, value, node) {
            // console.log(name, value, node);
            // console.log(group);
            const group = node.getContainer();
            const rect = group.get("children")[2]; // 顺序根据 draw 时确定
            const entity = group.get("children")[0];
            const entityName = group.get("children")[1];
            entity.attr("cursor", "pointer");
            entityName.attr("cursor", "pointer");

            if (name === "selected") {
              node.selected = value;
              if (value) {
                rect.attr("stroke", "RGBA(55,166,231,0.8)");

                // console.log(rect);
                // rect.attrs.stroke= "RGB(19,130,245,0.5)";
              } else {
                rect.attr("stroke", "RGBA(255,255,255,0)");
                // rect.attrs.stroke= "RGB(19,130,245,0)";
              }
            }
            if (name === "hover") {
              if (value) {
                rect.attr("stroke", "RGBA(55,166,231,0.8)");

                // console.log(rect);
                // rect.attrs.stroke= "RGB(19,130,245,0.5)";
              } else {
                if (node.selected) {
                  rect.attr("stroke", "RGBA(55,166,231,0.8)");

                  // console.log(rect);
                } else {
                  rect.attr("stroke", "RGBA(255,255,255,0)");
                }
                // rect.attrs.stroke= "RGB(19,130,245,0)";
              }
            }
          }
          // update(cfg, node) {
          //   console.log("cfg", node);
          // }
        },
        "image"
      );

      G6.registerEdge(
        "circle-running",
        {
          afterDraw(cfg, group) {
            // 获得当前边的第一个图形，这里是边本身的 path
            const shape = group.get("children")[0];
            // 边 path 的起点位置
            const startPoint = shape.getPoint(0);

            // 添加红色 circle 图形
            const circle = group.addShape("circle", {
              attrs: {
                x: startPoint.x,
                y: startPoint.y,
                fill: "#1890ff",
                r: 3
              }
            });

            // 对红色圆点添加动画
            circle.animate(
              {
                // 动画重复
                repeat: true,
                // 每一帧的操作，入参 ratio：这一帧的比例值（Number）。返回值：这一帧需要变化的参数集（Object）。
                onFrame(ratio) {
                  // 根据比例值，获得在边 path 上对应比例的位置。
                  const tmpPoint = shape.getPoint(ratio);
                  // 返回需要变化的参数集，这里返回了位置 x 和 y
                  return {
                    x: tmpPoint.x,
                    y: tmpPoint.y
                  };
                }
              },
              3000
            ); // 一次动画的时间长度
          }
        },
        "line"
      );
      const minimap = new Minimap({
        // container: "minimap",
        size: [100, 100],
        className: "minimap",
        type: "delegate"
        // delegateStyle: {
        //   x: 0,
        //   y: 0
        // }
      });
      // console.log("Minimap", minimap);

      let nodeW = $("#mountNode").width();
      let nodeH = $("#mountNode").height();

      const graph = new G6.Graph({
        container: "mountNode", // String | HTMLElement，必须，在 Step 1 中创建的容器 id 或容器本身
        width: nodeW, // Number，必须，图的宽度
        height: nodeH, // Number，必须，图的高度
        fitView: true,
        // fitViewPadding: [20, 40, 50, 20],
        autoPaint: true,
        plugins: [minimap],
        modes: {
          default: [
            "drag-canvas",
            "zoom-canvas",
            "drag-node",
            "click-select",
            {
              type: "brush-select",
              includeEdges: false,
              trigger: "ctrl"
            },
            {
              type: "tooltip",
              formatText(model) {
                // console.log(model);
                return `
                <div class="g6-tooltip-html">
                  <div>
                      <i class="el-icon-coin"></i> 
                    <span>
                      ${model.label}
                    </span>
                  </div>
                  <div>
                    <p>Type: ${model.type}</p>
                  </div>
                </div>
                `;
              }
            }
          ]
        },

        layout: {
          type: "dagre",
          rankdir: "LR", // 排列方式可选，默认为图的中心
          // align: "DL", //中心点 可选
          nodesep: 20, //节点间距 可选
          ranksep: 50 //层间距 可选
          // controlPoints: true //是否保留布局连线的控制点 可选
        },
        // defaultNode: {
        //   size: 45,
        //   style: {
        //     fill: "#DEE9FF",
        //     stroke: "#5B8FF9"
        //   }
        // },
        defaultEdge: {
          shape: "circle-running",
          style: {
            lineWidth: 2,
            stroke: "RGB(203,229,249)",
            endArrow: true,
            cursor: true
          }
        }
      });
      graph.on("node:mouseenter", function(evt) {
        const node = evt.item;
        const model = node.getModel();
        model.oriLabel = model.label;
        graph.setItemState(node, "hover", true);
        // graph.updateItem(node, {
        //   preRect: {
        //     show: true
        //   }
        // });
      });

      graph.on("node:mouseleave", function(evt) {
        const node = evt.item;
        const model = node.getModel();
        graph.setItemState(node, "hover", false);
        // graph.updateItem(node, {
        //   preRect: {
        //     show: true
        //   }
        // });
      });
      graph.data(this.g6Data); // 读取 Step 2 中的数据源到图上
      graph.render(); // 渲染图
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
        border: 1px solid #eee;
        box-shadow: 1px 1px 7px #eee;
        border-radius: 5px;
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
          width: 180px;
          display: flex;
          flex-direction: column;
          justify-content: center;
          margin-right: 30px;

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
          justify-self: end;
          flex: 1;
          display: flex;
          flex-wrap: wrap;

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

        #mountNode {
          position: relative;
          height: 100%;
        }

        .topology-tip {
          position: absolute;
          bottom: 3px;
          right: 0;
          font-size: 13px;
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
