<template>
  <div class="children" v-if="treeItem.open">
    <recursive-item @onAddEvent="hanldAddTree" :treeItem="treeItem" />
    <div v-if="treeItem.children && treeItem.children.length > 0">
      <list-recursive
        :treeItem="tree"
        v-for="tree in treeItem.children"
        :key="tree.id"
        @onDelete="handleDelete"
      />
    </div>
  </div>
</template>

<script>
import RecursiveItem from "./RecursiveItem.vue";

export default {
  name: "listRecursive",
  methods: {
    hanldAddTree(value) {
      // this.$emit("onDelete", { type: "delete", id: value.id });
    },
    handleDelete(value) {
      console.log(this.treeItem);
      const list = [...this.treeItem.children];
      console.log(list);
      list.forEach((item, index) => {
        if (item.id === value.id) {
          list.splice(index, 1);
          // this.treeArray.children.splice(index, 1);
        }
        
      });
   
    },
  },
  components: {
    "recursive-item": RecursiveItem,
  },
  props: {
    treeItem: {
      type: Object,
      default: {},
      required: true,
    },
  },
};
</script>

<style scoped>
.wraps {
  position: relative;
  width: 433px;
  height: auto;
  border-radius: 4px;
}

.wrap {
  position: relative;
  width: 433px;
  height: 30px;
  margin-bottom: 13px;
}
.wrap::before {
  content: "";
  position: absolute;
  width: 24px;
  right: 100%;
  top: 50%;
  transform: translateY(-50%);
  padding: 0;
  border-bottom: 2px solid rgba(220, 220, 220, 1);
}

.children {
  position: relative;
  padding-left: 28px;
}
.children::before {
  content: "";
  position: absolute;
  height: 100%;
  left: 15px;
  top: 0px;
  padding: 0;
  border-right: 2px solid rgba(220, 220, 220, 1);
}
.children:last-child::before {
  content: "";
  position: absolute;
  height: 23px;
  left: 15px;
  top: 0px;
  padding: 0;
  border-right: 2px solid rgba(220, 220, 220, 1);
}
</style>