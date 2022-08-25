<template>
  <div class="space_item">
    <div class="item">
      <div
        @click="handleToggle"
        class="info"
        @contextmenu.prevent="handleRightMouse"
      >
        <div class="number">{{ treeItem.floor }}</div>
        <h4 class="title">{{ treeItem.departmentId }}</h4>
        <p class="content">{{ treeItem.name }}</p>
      </div>
    </div>

    <Option @onAdd="handleAction" :treeItem="treeItem" :toggle="toggleOption" />
    <div
      @contextmenu.prevent
      @click="handleHidden"
      v-if="toggleOption"
      class="overlay"
    ></div>
  </div>
</template>

<script>
import Option from "./Option.vue";
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      toggleOption: false,
    };
  },
  methods: {
    handleToggle() {
      if (this.treeItem.children && this.treeItem.children.length > 0) {
        this.treeItem.children.forEach((item) => (item.open = !item.open));
      }
    },
    handleRightMouse() {
      this.toggleOption = true;
    },
    handleHidden() {
      this.toggleOption = false;
    },
    // action choose option
    handleAction(value) {
      //  this.$emit("onAddEvent",value)
      if (value.type === "add/close") {
        this.toggleOption = false;
      } else if (value.type === "add/department") {
        const id = uuidv4();
        this.treeItem.children.push({
          id,
          departmentId: value.id,
          name: value.name,
          children: [],
          open: false,
          floor: Number(this.treeItem.floor) + 1,
        });
        console.log(this.treeItem)
        this.toggleOption = false;
      }else if(value.type==="delete/delete"){
        this.$emit("onDelete",this.treeItem)
      }
    },
  },

  props: {
    treeItem: {
      type: Object,
      default: {},
      required: true,
    },
   
  },
  components: {
    Option,
  },
};
</script>

<style  scoped>
.space_item {
  position: relative;
  padding-top: 7px;
}
.info::before {
  content: "";
  position: absolute;
  width: 12px;
  right: 100%;
  top: 50%;
  transform: translateY(-50%);
  padding: 0;
  border-bottom: 2px solid rgba(220, 220, 220, 1);
}

.info {
  position: relative;
  flex-direction: row;
  display: flex;
  gap: 6px;
  align-items: center;
  padding: 0 7px;
  height: 100%;
  margin: 0;
  user-select: none;
  transition: 0.4s;
}
.info:hover {
  cursor: pointer;
}
.number {
  width: 18px;
  height: 18px;
  margin-left: 7px;
  background-color: #48647f;
  font-weight: 400;
  font-size: 12px;
  color: #fff;
  border-radius: 4px;
  line-height: 18px;
  margin: 0;
}
.title {
  font-weight: 400;
  font-size: 12px;
  min-width: 70px;
  margin: 0;
}
.content {
  font-size: 14px;
  margin: 0;
  flex: 1;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.item {
  height: 30px;
  border-radius: 4px;
  background-color: #f0f0f0;
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 10;
}
</style>