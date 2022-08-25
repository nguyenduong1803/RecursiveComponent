<template>
  <div>
    <div v-if="toggle" class="option">
      <ul class="listOption">
        <li @click="handleAction" class="optionItem">Thêm phòng ban</li>
        <li @click="handleDelete" class="optionItem">Xóa phòng ban</li>
        <li class="optionItem">Nâng level</li>
        <li class="optionItem">Giảm level</li>
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
    handleAction() {
      this.$emit("onAdd", "add/close");
      this.action = true;
    },
    handleDelete() {
      this.$emit("onAdd", {type:'delete/delete'});
    },
    handleSendValue(value) {
      this.action = false;
      this.$emit("onAdd", value);
    },
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
  },
  components: {
    Modal,
  },
};
</script>

<style  scoped>
.option {
  position: absolute;
  width: 150px;
  top: -20%;
  right: -12px;
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