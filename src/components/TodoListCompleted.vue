<template>
  <div class="todo-container">
    <h2 class="todo-list-completed">Выполненные задачи</h2>
    <ul v-if="taskListCompleted.length > 0" class="todo-list">
        <TodoItem
            v-for="item in taskListCompleted"
            :key="item.id"
            :id="item.id"
            :task_description="item.task_description"
            :priority_status="item.priority_status"
            :todo-delete-task="todoDeleteCompleted"
            @delete-complete="todoDeleteCompleted"
        />
    </ul>
    <p v-else>Выполненных задач нет.</p>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    components: {
        TodoItem
    },

    props: ['task-list-completed'],

    methods: {
        todoDeleteCompleted(id) {
            this.$emit('delete-complete', id);
        },
    },
}
</script>

<style>

</style>
