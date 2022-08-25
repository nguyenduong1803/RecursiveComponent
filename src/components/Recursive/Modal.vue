<template>
  <div @click="handleClose" :class="{ addClass: action }" class="overlay">
    <div @click.stop class="modal">
      <div class="headModal"><h2 class="title">Thêm mới phòng ban</h2></div>
      <form class="form">
        <div class="formInput">
          <label class="labelInput" for="name">Tên phòng ban</label>
          <input v-model="department" id="name" type="text" placeholder="Tên phòng ban..." />
        </div>
        <div class="formInput">
          <label class="labelInput" for="id">Mã phòng ban</label>
          <input
            id="id"
            type="text"
            v-model="departmentId"
            placeholder="Mã phòng ban (không bắt buộc)"
          />
        </div>
        <div class="wrapAction">
          <button @click.prevent="handleClose" class="btnBack">Hủy</button>
          <button @click.prevent="handleSubmitform" class="btnSave">Lưu</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      department:"",
      departmentId:""
    }
  },
  methods: {
    handleClose() {
      this.$emit("onSendValue", {type:"add/close"});
    },
    handleSubmitform() {
      this.$emit("onSendValue", {type:"add/department",name:this.department,id:this.departmentId});
    },
  },
  props: {
    action: {
      type: Boolean,
      default: false,
      required: true,
    },
  },
};
</script>

<style  scoped>
* {
  box-sizing: border-box;
}
.addClass.overlay {
  display: block;
}
.overlay {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(158, 158, 158, 0.4);
  z-index: 23;
}
.addClass .modal {
  display: block;
}
.modal {
  position: absolute;
  display: none;
  width: 502px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #ffffff;
  border: 1px solid #dcdcdc;
  border-radius: 10px;
}
.headModal {
  width: 100%;
  height: 48px;
  background: #48647f;
  border-radius: 4px 4px 0px 0px;
  padding-left: 33px;
}
.form {
  padding: 33px;
}
#name,
#id {
  height: 40px;
  width: 100%;
  border: 2px solid #c2c2c2;
  border-radius: 4px;
  padding-left: 11px;
}
#name::placeholder,
#id::placeholder {
  font-weight: 400;
  font-size: 12px;
  line-height: 14px;
  color: #48647f;
}
#name:focus,
#id:focus {
  outline: none;
}
.formInput {
  padding-bottom: 32px;
}
.title {
  font-weight: 700;
  font-size: 24px;
  line-height: 48px;
  margin: 0;
  color: #fff;
  text-align: left;
}
.labelInput {
  font-weight: 700;
  display: block;
  color: #48647f;
  text-align: left;
  margin-bottom: 5px;
}
.wrapAction {
  display: flex;
  justify-content: flex-end;
  gap: 20px;
}
.btnSave,
.btnBack {
  height: 40px;
  width: 108px;
  line-height: 30px;
  border: 2px solid #dcdcdc;
  border-radius: 4px;
  cursor: pointer;
}
.btnSave {
  background-color: rgba(72, 100, 127, 0.4);
  color: #fff;
}
.btnSave:hover {
  background-color: rgba(72, 100, 127, 0.5);
}
</style>