<template>
    <div class="todo-add-task">
      <input
        class="todo-add-input"
        type="text"
        placeholder="Напиши то, что тебе нужно сделать"
        v-model="addTaskInput"
        >
      <div class="todo-task-priority">
        <legend>Приоритет задачи:</legend>
        <div class="todo-priority-container">
          <input
            type="radio"
            v-model="priority"
            value="Low"
            name="priority-button"
          />
          <label for="low">Низкий</label>

          <input
            type="radio"
            v-model="priority"
            value="Medium"
            name="priority-button"
            />
          <label for="medium">Средний</label>

          <input
            type="radio"
            v-model="priority"
            value="High"
            name="priority-button" />
          <label for="high">Высокий</label>
        </div>
      </div>
      <button
        class="todo-add-button"
        @click="addTask"
        :disabled="addTaskInput.length === 0 || priority === null"
      >
        Добавить
      </button>
    </div>
</template>

<script>

export default {

    data() {
        return {
            addTaskInput: '',
            priority: null
        }
    },

    methods: {
        addTask() {
            this.$emit('add-task', this.addTaskInput, this.priority);
            this.addTaskInput = '';
            this.priority = null;
        }
    }
}
</script>

<style>
.todo-add-input {
    width: 290px;
    height: 20px;
    border: 1px solid black;
    border-radius: 10px;
    padding: 10px;
}

.todo-add-button {
    padding: 10px;
    border: 1px solid black;
    border-radius: 10px;
    background-color: cornflowerblue;
    font-size: 15px;
}

.todo-task-priority {
  margin-top: 10px;
  padding-bottom: 10px;
}

p, label {
  font: 14px;
}

input {
  margin: 0.4rem;
}

legend {
  font-size: 20px;
}

.todo-priority-container {
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
