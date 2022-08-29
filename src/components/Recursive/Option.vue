<template>
  <div>
    <div :style="{top:coordinate.y+'px',left:coordinate.x+'px'}" class="option">
      <ul class="listOption">
        <li @click="action=true" class="optionItem">Thêm phòng ban</li>
        <li @click="handleDelete" class="optionItem">Xóa phòng ban</li>
        <li @click="handleLevelup" class="optionItem">Nâng level</li>
        <li v-if="length>1" @click="handleLevelDown" class="optionItem">Giảm level</li>
      </ul>
    </div>
    <Modal :action="action" @onSendValue="handleSendValue" />
  </div>
</template>

<script>
import Modal from "./Modal.vue";
export default {
  data() {
    return {
      action: false,
    };
  },
  methods: {
    handleDelete() {
      this.$emit("onAdd", {type:'delete/delete'});
    },
    handleSendValue(value) {
      this.action = false;
      this.$emit("onAdd", value);
    },
    handleLevelup(){
      this.$emit("onAdd", {type:'level/up'});
    },
    handleLevelDown(){
      this.$emit("onAdd", {type:'level/down'});
    }
  },
  props: {
    toggle: {
      type: Boolean,
      default: false,
    },
    treeItem: {
      type: Object,
      default: {},
      required: true,
    },
    coordinate:{
      type:Object,
      default: {},
    },
    length:{
      Number
    }
  },
  components: {
    Modal,
  },
};
</script>

<style  scoped>
.option {
  position: fixed;
  width: 150px;
 
  box-shadow: 2px 4px 4px rgba(204, 204, 204, 0.5);
  border-radius: 4px;
  z-index: 20;
  background-color: #fff;
}
.optionItem {
  display: block;
  height: 36.46px;
  font-size: 12px;
  line-height: 36px;
  text-align: left;
  margin: 0;
  padding: 0 12px;
}
.listOption {
  margin: 0;
}
.optionItem:hover {
  border-radius: 4px;
  background-color: #48647f;
  color: #fff;
  cursor: pointer;
}
/* .overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 10;
  background-color: rgba(0,0,0,0.3);
} */
</style>