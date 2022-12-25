<template>
  <section>
    <transition-group tag="ul" name="list">
      <li v-for="(todoItem, index) in propsdata" :key="index" class="shadow">
        <i class="checkBtn fa-solid fa-check"></i>
        <span class="text">{{ todoItem }}</span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props: ["propsdata"],
  /* 삭제 
  data() {
    return { todoItems: [] }; 
  },*/

  /**************  App.vue로 이동
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },*/
  methods: {
    //전에 썼던 방식으로도 됨
    removeTodo: function (todoItem, index) {
      this.$emit("removeTodo", todoItem, index);
      //console.log("키" + todoItem + ", 밸류" + index); //-작동 잘 되는지 확인부터

      /* App.vue로 가져감
      localStorage.removeItem(todoItem); //이거 안하면 눈으로만 사라짐
      this.todoItems.splice(index, 1); */
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}

.text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis; /* 말줄임 적용 */
}
.checkBtn {
  line-height: 50px;
  color: #62acde;
  margin-right: 7px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
