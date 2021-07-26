<template>
  <div class="item" v-for="todo in todosList" :key="todo.title">
    <p class="title">
      {{ todo.title }}
    </p>

    <button class="delete-btn" @click="deleteTodo(todo)"></button>
  </div>
</template>

<script>
export default {
  props: ["savedTodos"],
  data() {
    return {
      todosList: this.savedTodos,
    };
  },

  methods: {
    deleteTodo(todo) {
      this.todosList.splice(todo.id, 1);
      if (this.todosList.length <= 1) {
        this.todosList.splice(todo.id);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.item {
  position: relative;
  display: flex;
  flex-direction: column;
  //gap: 40px;
  align-items: center;

  //padding: 20px;

  background: #fff;
  border-radius: 10px;

  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);

  &::before {
    content: "";
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    height: 50px;
    overflow: hidden;
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6,
      0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6,
      0 17px 2px -6px rgba(0, 0, 0, 0.2);
  }
}

.title {
  width: 90%;
  word-wrap: break-word;

  font-size: calc(14px + 10 * (100vw / 1440));
  text-align: center;
}
.delete-btn {
  position: absolute;
  z-index: 5;
  right: 10px;
  top: calc(50% - 20px);
  visibility: hidden;
  width: 40px;
  height: 40px;

  font-size: 30px;
  color: crimson;
  background: #fff;

  border: hidden;

  opacity: 0.3;
}
.item:hover .delete-btn {
  visibility: visible;
}

.delete-btn:hover {
  opacity: 1;
}
.delete-btn:before,
.delete-btn:after {
  position: absolute;
  top: 0;
  left: 15px;
  content: " ";
  height: 33px;
  width: 2px;
  background-color: #333;

  &:hover {
    background: #af5b5e;
  }
}
.delete-btn:before {
  transform: rotate(45deg);
}
.delete-btn:after {
  transform: rotate(-45deg);
}
</style>

