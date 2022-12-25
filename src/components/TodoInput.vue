<template>
  <div class="inputBox shadow">
    <input
      type="text"
      v-model="newTodoItem"
      placeholder="Type what you  have to do"
      v-on:keyup.enter="addTodo"
      maxlength="40"
    />
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fa-solid fa-plus"></i>
    </span>

    <!-- 모달팝업 설정 -->
    <AlertModal v-if="showModal">
      <h3 slot="header">경고</h3>
      <span slot="footer"
        >할 일을 입력하세요.
        <i
          class="closeModalBtn fa-solid fa-xmark"
          @click="showModal = false"
        ></i> </span
    ></AlertModal>
  </div>
</template>

<script>
import AlertModal from "./common/AlertModal.vue";

export default {
  data() {
    return { newTodoItem: "", showModal: false };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        const value = this.newTodoItem && this.newTodoItem.trim();
        //localStorage.setItem(value, value);직접 저장하지 않고
        this.$emit("addTodo", value); //상위(App.vue의 addTodo에 value전달)
        this.clearInput();
      } else {
        //텍스트 미입력시 모달팝업
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
  components: {
    AlertModal: AlertModal,
  },
};
</script>

<!-- scoped - 현재 컴포넌트만 사용 가능 -->
<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  text-align: center;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: inline-block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #62acde;
  font-size: 1.3rem;
  margin-left: 15px;
}
</style>
