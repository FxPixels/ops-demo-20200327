<template>
  <div id="mountNode"></div>
</template>
<script>
import G6, { Minimap } from "@antv/g6";
const Util = G6.Util;
const facility = require("../assets/images/数据库.png"); //设备
import $ from "jquery";

export default {
  data() {
    return {
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
  methods: {
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
  },
  mounted() {
    this.setTopology();

    let minimapEl = $(".minimap");
    minimapEl.append(`
      <p class="mini-text" style="text-align:center">缩略图</p>
    `);
  }
};
</script>
