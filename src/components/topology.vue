<template>
  <div style="width:100%; height:100%;">
    <div id="mountNode"></div>
    <div class="topology-node-tools">
      <!-- <span>工具栏</span> -->

      <radio-group v-model="modeType" size="mini" @change="modeChange">
        <radio :label="'default'" border>常用模式</radio>
        <radio :label="'addEdge'" border>连线模式</radio>
        <!-- <radio :label="'addNode'" border>节点模式</radio> -->
        <!-- <radio :label="9">备选项</radio> -->
      </radio-group>
    </div>

    <transition name="el-zoom-in-top">
      <div class="topology-contextmenu" v-show="showContextmenu">
        <p v-if="showContextmenuType == ''" @click="createNewNode">新建一个节点</p>
        <p
          v-if="showContextmenuType == 'node' && selectedtype == 'normal'"
          @click="createNewNodeAfterThisNode"
        >在本节点之后新建一个节点</p>
        <p v-if="showContextmenuType == 'node' && selectedtype == 'normal'">修改该节点</p>
        <p
          v-if="showContextmenuType == 'node' && selectedtype == 'normal'"
          @click="removeNodes"
        >删除该节点</p>
        <p v-if="showContextmenuType == 'edge'" @click="removeEdge">删除该连接</p>
        <p
          v-if="
            showContextmenuType == 'node' &&
              selectedtype == 'multi' &&
              selectedNodes.length == 2
          "
          @click="createEdge"
        >从另一个节点连接到本节点</p>
        <p
          v-if="showContextmenuType == 'node' && selectedtype == 'multi'"
          @click="removeNodes"
        >删除所选节点</p>
      </div>
    </transition>
  </div>
</template>
<script>
import G6, { Minimap, Grid } from "@antv/g6";
const Util = G6.Util;
const facility = require("../assets/images/数据库.png"); //设备
import $ from "jquery";
import { Button, Radio, RadioGroup } from "element-ui";
import CollapseTransition from "element-ui/lib/transitions/collapse-transition";
import "element-ui/lib/theme-chalk/base.css";

export default {
  components: {
    Button,
    CollapseTransition,
    Radio,
    RadioGroup
  },
  data() {
    return {
      showContextmenu: false,
      addedCount: 50,
      showContextmenuType: "",
      selectedtype: "normal",
      graph: null,
      mouseInfo: null,
      selectedNodes: [],
      selectedTargetNode: null,
      selectedEdge: null,
      endAddEdge: false,
      modeType: "default",
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
            // x: 700, // Number，可选，节点位置的 x 值
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
  methods: {
    // 设置拓扑图
    setTopology() {
      // Register a custom behavior: add a node when user click the blank part of canvas
      const that = this;

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

      G6.registerNode(
        "DomNode",
        {
          draw: (cfg, group) => {
            const size = cfg.size;
            // console.log(cfg);
            return group.addShape("dom", {
              attrs: {
                width: size,
                height: size + 20,
                // 传入 DOM 的 html
                html: `
                <div>
                    <img src="${cfg.img}"/>
                    <p>${cfg.label}</p>
                </div>
                `
              },
              name: "dom-shape",
              draggable: true
            });
          }
        },
        // 注意这里继承了 'single-edge'
        "single-node"
      );

      G6.registerEdge(
        "circle-running",
        {
          afterDraw(cfg, group) {
            // 获得当前边的第一个图形，这里是边本身的 path
            const shape = group.get("children")[0];
            const sline = group.get("children")[1];

            // sline.attr("cursor", "pointer");
            // console.log(group.get("children")[1]);
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
        "quadratic"
      );

      // Register a custom behavior: click two end nodes to add an edge
      G6.registerBehavior("click-add-edge", {
        // Set the events and the corresponding responsing function for this behavior
        getEvents() {
          return {
            "node:click": "onClick", // The event is canvas:click, the responsing function is onClick
            mousemove: "onMousemove", // The event is mousemove, the responsing function is onMousemove
            "edge:click": "onEdgeClick" // The event is edge:click, the responsing function is onEdgeClick
          };
        },
        // The responsing function for node:click defined in getEvents
        onClick(ev) {
          const self = this;
          const node = ev.item;
          const graph = self.graph;
          // The position where the mouse clicks
          const point = { x: ev.x, y: ev.y };
          const model = node.getModel();
          if (self.addingEdge && self.edge) {
            graph.updateItem(self.edge, {
              target: model.id
            });

            self.edge = null;
            self.addingEdge = false;
            that.endAddEdge = true;
          } else {
            // Add anew edge, the end node is the current node user clicks
            self.edge = graph.addItem("edge", {
              source: model.id,
              target: point,
              id: "edge" + that.addedCount,
              label: "连接" + that.addedCount,
              labelCfg: {
                autoRotate: true,
                refY: 10,
                style: {
                  fontSize: 14
                }
              }
            });
            that.commonOperation();
            self.addingEdge = true;
          }
        },
        // The responsing function for mousemove defined in getEvents
        onMousemove(ev) {
          const self = this;

          // The current position the mouse clicks
          const point = { x: ev.x, y: ev.y };
          if (self.addingEdge && self.edge) {
            // Update the end node to the current node the mouse clicks
            self.graph.updateItem(self.edge, {
              target: point
            });
          }
        },
        // The responsing function for edge:click defined in getEvents
        onEdgeClick(ev) {
          const self = this;
          const currentEdge = ev.item;
          if (self.addingEdge && self.edge === currentEdge) {
            self.graph.removeItem(self.edge);
            self.edge = null;
            self.addingEdge = false;
          }
        }
      });

      let nodeW = $("#mountNode").width();
      let nodeH = $("#mountNode").height();
      // console.log(nodeW, nodeH);

      let ratio = nodeW / nodeH;
      let minimapH = 120;

      // const mgrid = new G6.Grid();
      const minimap = new Minimap({
        // container: "minimap",
        size: [minimapH / ratio, minimapH],
        // size: [70, 150],
        className: "minimap",
        type: "delegate"
        // delegateStyle: {
        //   x: 0,
        //   y: 0
        // }
      });
      // console.log("Minimap", minimap);
      this.graph = new G6.Graph({
        container: "mountNode", // String | HTMLElement，必须，在 Step 1 中创建的容器 id 或容器本身
        width: nodeW, // Number，必须，图的宽度
        height: nodeH, // Number，必须，图的高度
        fitView: true,
        // fitViewPadding: [20, 40, 50, 20],
        // autoPaint: true,
        plugins: [
          // mgrid, 
          minimap],
        // renderer: "svg",
        modes: {
          default: [
            "drag-canvas",
            "zoom-canvas",
            "drag-node",
            "click-select",
            {
              type: "brush-select",
              includeEdges: false,
              // trigger: "ctrl",
              onSelect: nodes => {
                this.selectedNodes = nodes;
                this.selectedtype = "multi";
              }
            },
            {
              type: "tooltip",
              formatText(model) {
                // console.log(model);
                return `
                <div class="g6-tooltip-html" id="g6-tooltip-${model.id}">
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
          ],
          addEdge: [
            "click-add-edge",
            "click-select",
            "drag-canvas",
            "zoom-canvas",
            {
              type: "brush-select",
              includeEdges: false,
              // trigger: "ctrl",
              onSelect: nodes => {
                this.selectedNodes = nodes;
                this.selectedtype = "multi";
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

      this.graph.on("canvas:click", evt => {
        // evt.preventDefault();
        evt.stopPropagation();
        this.showContextmenuType = "";
        this.showContextmenu = false;
        // this.graph.setMode("default");
        this.selectedtype = "normal";
        this.selectedNodes = [];
      });

      this.graph.on("canvas:contextmenu", evt => {
        evt.preventDefault();
        evt.stopPropagation();

        // this.selectedtype = "normal";

        $(".topology-contextmenu").css("top", evt.canvasY + "px");
        $(".topology-contextmenu").css("left", evt.canvasX + "px");
        this.showContextmenuType = "";
        this.selectedNodes = [];
        this.mouseInfo = evt;
        this.showContextmenu = true;
      });

      this.graph.on("node:contextmenu", evt => {
        evt.preventDefault();
        evt.stopPropagation();
        $(".topology-contextmenu").css("top", evt.canvasY + "px");
        $(".topology-contextmenu").css("left", evt.canvasX + "px");
        this.showContextmenuType = "node";
        this.mouseInfo = evt;
        if (this.selectedtype == "normal") {
          this.selectedNodes = [];
          this.selectedNodes.push(evt.item);
        } else if (
          this.selectedNodes.length == 2 &&
          this.selectedtype == "multi"
        ) {
          this.selectedTargetNode = evt.item;
        }

        this.showContextmenu = true;
      });

      this.graph.on("edge:contextmenu", evt => {
        evt.preventDefault();
        evt.stopPropagation();

        // this.selectedtype = "normal";

        $(".topology-contextmenu").css("top", evt.canvasY + "px");
        $(".topology-contextmenu").css("left", evt.canvasX + "px");
        this.showContextmenuType = "edge";
        this.selectedEdge = evt.item;
        console.log(evt);
        this.mouseInfo = evt;
        this.showContextmenu = true;
      });

      this.graph.on("node:mouseenter", evt => {
        const node = evt.item;
        const model = node.getModel();
        model.oriLabel = model.label;
        this.graph.setItemState(node, "hover", true);
        // graph.updateItem(node, {
        //   preRect: {
        //     show: true
        //   }
        // });
      });

      this.graph.on("node:mouseleave", evt => {
        const node = evt.item;
        const model = node.getModel();
        this.graph.setItemState(node, "hover", false);
        // graph.updateItem(node, {
        //   preRect: {
        //     show: true
        //   }
        // });
      });
      this.graph.data(this.g6Data); // 读取 Step 2 中的数据源到图上
      this.graph.render(); // 渲染图
    },

    // 切换模式
    modeChange(type) {
      this.modeType = type;
      this.graph.setMode(type);
      if (type != "addEdge") {
        if (!this.endAddEdge) {
          let index = this.addedCount - 1;
          const item = this.graph.findById("edge" + index);
          // console.log("item","edge" + index, item);
          this.graph.removeItem("edge" + index);
        } else {
          this.endAddEdge = false;
        }
      }
    },

    // 从一节点新增下级节点
    createNewNodeAfterThisNode() {
      let sourceId = "node" + this.addedCount;

      this.addItem("node", {
        id: sourceId, // String，该节点存在则必须，节点的唯一标识
        label: "服务器" + this.addedCount,
        img: facility,
        type: "myimg",
        size: 70,
        // name: "node" + this.addedCount,
        // draggable: true,
        labelCfg: {
          style: {
            fontSize: 14
          }
        },
        x: this.mouseInfo.x + 150, // Number，可选，节点位置的 x 值
        y: this.mouseInfo.y // Number，可选，节点位置的 y 值
      });

      this.addItem("edge", {
        source: this.selectedNodes[0].defaultCfg.id, // String，必须，起始点 id
        target: sourceId, // String，必须，目标点 id
        // style: {
        //   endArrow: true,
        //   // stroke: "RGB(95,99,104)",
        //   lineWidth: 3
        // },
        label: "连接" + ++this.addedCount,
        labelCfg: {
          autoRotate: true,
          refY: 10,
          style: {
            fontSize: 14
          }
        }
      });

      this.commonOperation();
    },

    // 新增节点
    createNewNode() {
      this.addItem("node", {
        id: "node" + this.addedCount, // String，该节点存在则必须，节点的唯一标识
        label: "服务器" + this.addedCount,
        img: facility,
        type: "myimg",
        size: 70,
        // name: "node" + this.addedCount,
        // draggable: true,
        labelCfg: {
          style: {
            fontSize: 14
          }
        },
        x: this.mouseInfo.x, // Number，可选，节点位置的 x 值
        y: this.mouseInfo.y // Number，可选，节点位置的 y 值
      });

      this.commonOperation();
    },

    // 移除节点
    removeNodes() {
      for (let i = 0; i < this.selectedNodes.length; i++) {
        let item = this.selectedNodes[i].defaultCfg;
        this.graph.removeItem(item.id);
        $(`#g6-tooltip-${item.id}`)
          .parent()
          .remove();
      }

      this.selectedNodes = [];
      this.commonOperation();
    },

    // 新增连线
    createEdge() {
      let sourceNodeId = null;
      let index = null;
      for (let i = 0; i < this.selectedNodes.length; i++) {
        if (
          this.selectedTargetNode.defaultCfg.id ==
          this.selectedNodes[i].defaultCfg.id
        ) {
          index = i;
        }
      }

      if (index == 1) {
        sourceNodeId = this.selectedNodes[0].defaultCfg.id;
      } else if (index == 0) {
        sourceNodeId = this.selectedNodes[1].defaultCfg.id;
      }

      this.addItem("edge", {
        source: sourceNodeId, // String，必须，起始点 id
        target: this.selectedTargetNode.defaultCfg.id, // String，必须，目标点 id
        // style: {
        //   endArrow: true,
        //   // stroke: "RGB(95,99,104)",
        //   lineWidth: 3
        // },
        label: "连接" + this.addedCount,
        labelCfg: {
          autoRotate: true,
          refY: 10,
          style: {
            fontSize: 14
          }
        }
      });

      this.commonOperation();
    },

    // 删除连线
    removeEdge() {
      this.graph.removeItem(this.selectedEdge.defaultCfg.id);
      this.commonOperation();
    },
    addItem(type, config) {
      this.graph.addItem(type, config);
      // this.commonOperation();
    },

    // 操作之后要做的事情
    commonOperation() {
      this.addedCount++;
      this.showContextmenu = false;
      this.showContextmenuType = "";
      this.selectedTargetNode = null;

      this.graph.paint();
      this.graph.setAutoPaint(true);
    }
  },
  mounted() {
    this.setTopology();

    let minimapEl = $(".minimap");
    minimapEl.append(`
      <p class="mini-text" style="text-align:center">缩略图</p>
    `);

    // console.log();
    // $(".g6-grid")
    //   .parent()
    //   .css({ "z-index": 0 });
    $(".g6-grid").css({
      cssText: "transform: matrix(1, 0, 0, 1, 0, 0) ！important;"
    });

    // this.graph.refresh();
  }
};
</script>

<style lang="less">
#mountNode {
  position: relative;
  height: 100%;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  z-index: 1;
}

.topology-node-tools {
  position: absolute;
  top: 0;
  right: 0;
  font-size: 13px;
  z-index: 1;

  .el-radio {
    margin-right: 0 !important;
  }
  .el-button--mini {
    padding: 6px;
  }
}

.topology-contextmenu {
  background-color: #fff;
  padding: 10px 0;
  position: absolute;
  font-size: 12px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  border: 1px solid #ebeef5;
  min-width: 188px;
  z-index: 100;
  z-index: 2;

  & > p {
    padding: 0px 20px;
    line-height: 24px;

    &:hover {
      background-color: #edf5ff;
      color: #66b1ff;
      cursor: pointer;
    }
  }
}
</style>
