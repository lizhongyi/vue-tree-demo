<template>
  <div>
    <div v-for="(item,index) in list" :key="index">
      <slot></slot>

      <p :style="'margin-left:'+(item.level)*30+'px'" @click="changeStatus(item)">
        <span v-if="item.children && item.children.length">
          <span>{{ item.isExpand ?'关闭':'展开'}}</span>
        </span>
        {{item.name}} level-{{item.level}}
      </p>
      <tree-menus v-if="item.isExpand " :list="item.children"></tree-menus>
    </div>
  </div>
</template>
 <style>
ul {
  margin-top: 50px;
  padding-left: 20px !important;
}
</style>
<script>
// import treeMenus from './treeMenu2.vue'
export default {
  name: "treeMenus",
  props: {
    list: Array
  },
  data() {
    return {
      scopesDefault: [],
      scopes: []
    };
  },

  methods: {
    changeStatus(item) {
      if (item.isExpand == true) {
        this.$set(item, "isExpand", false);
      } else {
        this.$set(item, "isExpand", true);
      }
    },
    scope() {
      this.list.forEach((item, index) => {
        // this.scopesDefault[index] = false;
        if ("children" in item) {
          this.scopes[index] = true;
          console.log(item, index);
        } else {
          this.scopes[index] = false;
        }
      });
      console.log(this.scopesDefault);
    }
  },
  created() {
    this.scope();
  }
};
</script>