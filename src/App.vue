<template>
  <div class="todo">
    <div class="todo__taskbar">
      <form action=""></form>
      <input
        type="text"
        class="todo__input"
        v-model.trim="title"
        @keyup.enter.prevent="saveTodo"
      />
      <textarea
        name="description"
        id="description"
        class="todo__description"
        v-model.trim="description"
      >
      </textarea>
      <div class="todo__btn-wrapper">
        <button class="todo__btn" @click="saveTodo">Save</button>
        <button class="todo__btn" @click="deleteAllTodos">Clear All</button>
      </div>
    </div>
    <div class="todo__list">
      <todo-item :savedTodos="savedTodos" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
      title: "",
      description: "",
      savedTodos: [],
    };
  },

  methods: {
    saveTodo() {
      let todo = {};
      if (this.title.length > 0 || this.description.length > 0) {
        todo["id"] = this.count;
        todo["title"] = this.title;
        todo["description"] = this.description;

        this.title = "";
        this.description = "";
        this.count++;

        this.savedTodos.push(todo);
      }
    },

    deleteAllTodos() {
      this.savedTodos.splice(0);
      this.count = 0;
    },
  },
};
</script>

<style lang="scss">
html {
  font-size: 30px;
}

.todo {
  display: flex;
  flex-direction: column;

  align-items: center;

  width: 90vw;
  min-height: 80vh;
  margin: 3vh 3vw;
  padding: 50px 0;

  //border: 12px solid #207;

  &__btn-wrapper {
    display: flex;
    gap: 4vw;
  }

  &__taskbar {
    display: flex;
    flex-direction: column;
    gap: 40px;
    align-items: center;

    width: 30vw;
    margin-bottom: 5vh;
    padding: 20px;

    border: 6px solid #207567;
    border-radius: 10px;
  }

  &__input {
    width: 90%;
    height: 50px;

    border: 3px solid;

    &_brd-red {
      border: red;
    }
  }
  &__description {
    min-width: 90%;
    max-width: 90%;
    height: 100px;

    border: 3px solid;
  }
  &__btn {
    width: 120px;
    height: 60px;

    background: #224636;
    color: #fff;
    border-radius: 50px;

    transition: all 0.3s ease-in-out;

    font-size: 22px;

    &:hover {
      cursor: pointer;
      background: #6baf92;
    }
  }

  &__list {
    display: flex;
    flex-direction: column;
    gap: 4vh;
    width: 30vw;
    padding: 20px;
  }
}
</style>
