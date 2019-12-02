<template>
  <div>
    <my-trees :list="list"></my-trees>
  </div>
</template>
<script>
import myTrees from "./treeMenus";
export default {
  components: {
    myTrees
  },
  data() {
    return {
      list: [
        {
          name: "node 0-0",
          children: [
            { name: "node 0-0-1" },
            {
              name: "node 0-0-1-0",
              children: [
                {
                  name: "node 0-0-1-0-0",
                  children: [{ name: "node 0-0-1-0-0-0" }]
                }
              ]
            }
          ]
        },
        { name: "node 0-1" },
        {
          name: "node 0-2",
          children: [{ name: "node 0-2-0" }, { name: "node 0-2-1" }]
        }
      ]
    };
  },
  methods: {
    initTreeData() {
      let tempData = JSON.parse(JSON.stringify(this.list));
      let reduceDataFunc = (data, level) => {
        data.map((m, i) => {
          m.isExpand = true; //默认全部展开
          m.children = m.children || [];
          m.level = level;
          m.bLeft = level === 1 ? 40 : (level - 2) * 20 + 40;
          m.Experience = m.Experience || "无";
          if (m.children.length > 0) {
            reduceDataFunc(m.children, level + 1);
          }
        });
      };
      reduceDataFunc(tempData, 1);
      console.log("处理后的:", tempData);
      this.list = tempData;
    }
  },
  mounted() {
    this.initTreeData();
  }
};
</script>