<template>
  <div class="todo-container">
    <h2 class="todo-list-completed">Список задач</h2>
    <ul v-if="taskList.length > 0" class="todo-list">
      <TodoItem
        v-for="item in taskList"
        :key="item.id"
        :id="item.id"
        :task_description="item.task_description"
        :priority_status="item.priority_status"
        @delete="todoDelete"
        />
    </ul>
    <p v-else>Список пуст. Добавьте задачи.</p>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    components: {
        TodoItem
    },

    props: ['task-list'],

    methods: {
      todoDelete(id) {
        this.$emit('delete', id)
      }
    }
}
</script>

<style>
.todo-container {
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  width: 800px;
  border: 1px solid black;
  border-radius: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
}
</style>
