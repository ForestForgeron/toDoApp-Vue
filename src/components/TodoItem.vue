<template>
  <div class="item" v-for="todo in todosList" :key="todo.id">
    <p class="title">
      {{ todo.title }}
    </p>
    <p class="description">
      {{ todo.description }}
    </p>
    <button class="delete-btn" @click="deleteTodo(todo)">x</button>
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
  gap: 40px;
  align-items: center;

  padding: 20px;

  border-radius: 10px;
  border: 1px solid black;
  border: 3px solid #207;
}

.title,
.description {
  width: 90%;
  word-wrap: break-word;

  font-size: 20px;
}
.delete-btn {
  position: absolute;
  z-index: 5;
  right: 10px;
  top: calc(50% - 15px);
  visibility: hidden;
  width: 30px;
  height: 30px;

  font-size: 30px;

  border: hidden;
}
.item:hover .delete-btn {
  visibility: visible;
}
</style>

