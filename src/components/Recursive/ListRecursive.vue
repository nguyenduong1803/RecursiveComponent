<template>
  <div draggable="true" class="children" v-if="treeItem.open">
    <recursive-item
      @onAddEvent="handleAction"
      :treeItem="treeItem"
      :length="length"
    />
    <div v-if="treeItem.children && treeItem.children.length > 0">
      <list-recursive
        :treeItem="tree"
        v-for="tree in treeItem.children"
        :key="tree.id"
        @onActionList="handleActionList"
        :length="treeItem.children.length"
      />
    </div>
  </div>
</template>

<script>
import RecursiveItem from "./RecursiveItem.vue";

export default {
  name: "listRecursive",
  data() {
    return {
      // floor: this.treeItem.floor,
      id: null,
    };
  },
  methods: {
    // get value from recursive Item
    handleAction(value) {
      if (value.type === "delete/delete") {
        this.$emit("onDelete", { type: "delete/delete", id: value.tree.id });
        this.$emit("onActionList", {
          type: "delete/delete",
          id: value.tree.id,
        });
      } else if (value.type === "level/up") {
        this.$emit("onActionList", value);
      } else if (value.type === "level/down") {
        this.$emit("onActionList", value);
      }
    },
    // handle after handleActionList send $emit value
    handleActionList(value) {
      if (value.type === "delete/delete") {
        this.deleteTree(value.id);
      } else if (value.type === "level/up") {
        // const newTree = { ...value.tree, floor: value.tree.floor -1 };
        // this.treeItem.children.push(newTree);
        // this.deleteTree(value.id);
      } else if (value.type === "level/down") {
        console.log(value.tree);
        // this.floor = value.tree.floor;
        const list = [...this.treeItem.children];
        list.forEach((item, index) => {
          if (item.id === value.id) {
            if (list[index - 1]) {
              list[index - 1].children.push(value.tree);
              list[index - 1].children.forEach((item) => {
                item.open === true;
                this.id = list[index - 1].id;

                // item.children.forEach((items) => {
                //   items.floor = items.floor + 1;
                // });
              });
              console.log(item.children);
            } else {
              const lastIndex = list[list.length - 1];
              lastIndex.children.push(value.tree);
              lastIndex.children.forEach((item) => {
                item.open === true;
              });
              this.id = lastIndex.id;
              console.log(item.children);
            }
            list.splice(index, 1);
          }
        });

        this.treeItem.children = list;
      }
    },
    deleteTree(id) {
      const list = [...this.treeItem.children];
      list.forEach((item, index) => {
        if (item.id === id) {
          list.splice(index, 1);
        }
      });
      this.treeItem.children = list;
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
    length: {
      type: Number,
    },
   
  },
  watch: {
    // id(newValue) {
    //   console.log(newValue);
    //   console.log(this.treeItem);
    //   this.treeItem.children.forEach((item) => {
    //     if (item.id === newValue) {
    //       item.children.forEach((item) => {
    //         item.floor = item.floor + 1
    //       });
    //     }
    //   });
    // },
    floor(newValue) {
      console.log(newValue);
      console.log(this.treeItem);
      
    },
    treeItem(newValue) {
      console.log(newValue);
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