<template>
  <div class="todo">
    <div class="todo__taskbar">
      <input
        type="text"
        class="todo__input"
        maxlength="93"
        placeholder="What do you want to do?"
        v-model.trim="title"
        @keyup.enter.prevent="saveTodo"
      />
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

      savedTodos: [],
    };
  },

  methods: {
    saveTodo() {
      let todo = {};
      if (this.title.length > 0) {
        todo["id"] = this.count;
        todo["title"] = this.title;

        this.savedTodos.push(todo);

        this.title = "";

        this.count++;
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
html,
body {
  margin: 0;
  padding: 0;

  background: #f5f5f5;
}

html {
  font: 14px "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 30px;
  font-weight: 300;
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

    width: 40vw;

    //padding: 20px;

    //border: 6px solid #207567;
    border-radius: 15px;

    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
  }

  &__input {
    width: 100%;
    height: 65px;

    padding: 0 20px;
    font-size: calc(14px + 10 * (100vw / 1440));

    border-radius: 15px;

    border: none;
  }
  &__description {
    display: none;
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
    width: 40vw;
    padding: 20px;
  }
}

@media screen and (max-width: 760px) {
  .todo {
    &__taskbar,
    &__list {
      width: 70vw;
    }
  }
}
</style>
