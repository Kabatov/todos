<template>
    <div class="todo-add-task">
      <input
        class="todo-add-task__input"
        placeholder="Напиши то, что тебе нужно сделать"
        v-model="inputTask"
        >
      <form class="todo-add-task__form">
        <h2>Приоритет задачи:</h2>
        <div class="todo-add-task__priority">
          <label>
            <input
              class="todo-add-task__input-priority"
              type="radio"
              v-model="priority"
              value="Low"
            />
            Низкий
          </label>
          <label>
            <input
              class="todo-add-task__input-priority"
              type="radio"
              v-model="priority"
              value="Medium"
            />
            Средний
          </label>
          <label>
            <input
              class="todo-add-task__input-priority"
              type="radio"
              v-model="priority"
              value="High"
            />
            Высокий
          </label>
        </div>
      </form>
      <button
        class="todo-add-task__button"
        @click="addTask"
        :disabled="!inputTask.length || !priority"
      >
        Добавить
      </button>
    </div>
</template>

<script>

export default {

    data() {
        return {
          inputTask: '',
          priority: null
        }
    },

    methods: {
      addTask() {
            this.$emit('add-task', {
              taskDescription: this.inputTask,
              priorityStatus: this.priority
            });
            this.inputTask = '';
            this.priority = null;
        }
    }
}
</script>

<style>

.todo-add-task__input {
    width: 290px;
    height: 20px;
    border: 1px solid black;
    border-radius: 10px;
    padding: 10px;
}

.todo-add-task__button {
    padding: 10px;
    border: 1px solid black;
    border-radius: 10px;
    background-color: cornflowerblue;
    font-size: 15px;
}

.todo-add-task__form {
  margin-top: 10px;
  padding-bottom: 10px;
}

.todo-add-task__input-priority {
  margin: 0.4rem;
}

.todo-add-task__priority {
  width: 300px;
  text-align: center;
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  padding: 5px;
  border: 1px solid black;
  border-radius: 10px;
}

</style>
