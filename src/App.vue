<template>
  <div class="container">
    <TodoTitle />
    <TodoAddTask @add-task="addTask"/>
    <TodoList
      :task-list="taskList"
      @delete="todoDelete"
    />
    <TodoListCompleted
      :task-list-completed="taskListCompleted"
      @delete-complete="todoCompletedButton"
    />
  </div>
</template>

<script>
import TodoAddTask from './components/TodoAddTask.vue';
import TodoList from './components/TodoList.vue';
import TodoListCompleted from './components/TodoListCompleted.vue';
import TodoTitle from './components/TodoTitle.vue';

export default {
  components: {
    TodoTitle,
    TodoList,
    TodoAddTask,
    TodoListCompleted
  },

  data() {
    return {
      taskList: [],
      taskListCompleted: []
    }
  },

  watch: {
    taskList: {
      handler() {
        const priorityOrder = { High: 1, Medium: 2, Low: 3 }

        this.taskList.sort((a, b) => priorityOrder[a.priority_status] - priorityOrder[b.priority_status]);
      },
      deep: true
    }

  },

  methods: {
    addTask(task_description, priority_status) {
      const newTask = {
        id: Date.now(),
        task_description,
        priority_status
      };
      this.taskList.push(newTask);
    },

    todoDelete(id) {
      const itemIndex = this.taskList.findIndex(item => item.id === id)

      if (itemIndex !== -1) {
        this.taskListCompleted.push(this.taskList[itemIndex])
      }

      this.taskList = this.taskList.filter((task) => id !== task.id);
    },

    todoCompletedButton(id) {
      const itemIndex = this.taskListCompleted.findIndex(item => item.id === id)

      if (itemIndex !== -1) {
        this.taskList.push(this.taskListCompleted[itemIndex])
      }

      this.taskListCompleted = this.taskListCompleted.filter((task) => id !== task.id);
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
