<template>
  <div class="todo">
    <div class="todo__taskbar">
      <input
        type="text"
        class="todo__input"
        v-model.trim="message"
        placeholder="Введите задачу..."
        @keyup.enter.prevent="saveMessage"
      />
      <div class="todo__btn-wrapper">
        <button class="todo__btn" @click="saveMessage">Save</button>
        <button class="todo__btn" @click="deleteAllMsg">Clear All</button>
      </div>
    </div>
    <div class="todo__list">
      <div class="todo__item" v-for="message in savedMessages" :key="message">
        <p class="todo__msg">
          {{ message }}
        </p>
        <button class="todo__btn" @click="deleteMessage">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "",
      savedMessages: [],
    };
  },

  methods: {
    saveMessage() {
      if (this.message.length > 0) {
        this.savedMessages.push(this.message);
        this.message = "";
      }
    },

    deleteMessage() {
      const messageId = this.savedMessages.indexOf(this.message);
      this.savedMessages.splice(messageId, 1);
    },

    deleteAllMsg() {
      this.savedMessages = [];
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

  border: 12px solid #207;

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

  &__item {
    display: flex;
    flex-direction: column;
    gap: 40px;
    align-items: center;

    padding: 20px;

    border-radius: 10px;
    border: 1px solid black;
    border: 3px solid #207;
  }

  &__msg {
    width: 100%;
    word-wrap: break-word;

    font-size: 20px;
  }
}
</style>
