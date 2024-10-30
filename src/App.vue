<template>
  <div class="container">
    <TodoTitle />
    <TodoAddTask @add-task="pushTask"/>
    <TodoList
    :task-list="taskList"
    @delete="todoDelete"
    />
  </div>
</template>

<script>
import TodoAddTask from './components/TodoAddTask.vue';
import TodoList from './components/TodoList.vue';
import TodoTitle from './components/TodoTitle.vue';

export default {
  components: {
    TodoTitle,
    TodoList,
    TodoAddTask
  },

  data() {
    return {
      taskList: [],
    }
  },

  methods: {
    pushTask(task_description, priority_status) {
      const newTask = {
        id: Date.now(),
        task_description: task_description,
        priority_status: priority_status
      };
      this.taskList.push(newTask);
    },

    todoDelete(id) {
      this.taskList = this.taskList.filter((task) => id !== task.id)
    }
  }
}
</script>

<style>
.container {
  text-align: center;
  margin: 0 auto;
}

</style>
