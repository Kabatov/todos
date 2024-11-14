<template>
  <div class="todo-list">
    <h2 class="todo-list__title">{{ title }}</h2>
    <ul v-if="taskList.length > 0" class="todo-list__items">
      <TodoItem
        v-for="item in taskList"
        :key="item.id"
        :id="item.id"
        :taskDescription="item.taskDescription"
        :priorityStatus="item.priorityStatus"
        @delete="todoDelete"
        @update-task="updateTask"
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

    props: ['task-list', 'title'],

    methods: {
      todoDelete(id) {
        this.$emit('delete-todo', id)
      },

      updateTask({description, id}) {
        this.$emit('update-task', {
                description,
                id
            })
      }
    }
}
</script>

<style>
.todo-list {
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  width: 800px;
  border: 1px solid black;
  border-radius: 20px;
}

.todo-list__items {
  list-style: none;
  padding: 0;
}
</style>
