<template>
  <div class="todo-app">
    <TodoTitle />
    <TodoAddTask @add-task="addTask"/>
    <ListSwitcher @change-active-tab="changeActiveTab"/>
    <keep-alive>
      <div>
        <TodoList
          v-if="isActiveTaskList"
          :task-list="taskList"
          @delete-todo="(id) => deleteTodo(id, 'taskList', 'taskListCompleted')"
          :title="'Невыполненные Задачи'"
          @update-task="updateTask"
        />
        <TodoList
          v-if="isActiveTaskListCompleted"
          :task-list="taskListCompleted"
          @delete-todo="(id) => deleteTodo(id, 'taskListCompleted', 'taskList')"
          :title="'Выполненные Задачи'"
        />
      </div>
    </keep-alive>
  </div>
</template>

<script>
import TodoAddTask from './components/TodoAddTask.vue';
import TodoList from './components/TodoList.vue';
import TodoTitle from './components/TodoTitle.vue';
import ListSwitcher from './components/ListSwitcher.vue';

export default {
  components: {
    TodoTitle,
    TodoList,
    TodoAddTask,
    ListSwitcher
  },

  data() {
    return {
      taskList: [],
      taskListCompleted: [],
      isActiveTaskListTab: 'task-list'
    }
  },

  computed: {
    isActiveTaskList() {
      return this.isActiveTaskListTab === 'task-list';
    },

    isActiveTaskListCompleted() {
      return this.isActiveTaskListTab === 'task-list-completed';
    }
  },

  watch: {
    taskList: {
      handler() {
        const priorityOrder = { High: 1, Medium: 2, Low: 3 }

        this.taskList.sort((a, b) => priorityOrder[a.priorityStatus] - priorityOrder[b.priorityStatus]);
      },
      deep: true
    }
  },

  methods: {
    addTask({taskDescription, priorityStatus}) {
      const newTask = {
        id: Date.now(),
        taskDescription,
        priorityStatus
      };
      this.taskList.push(newTask);
    },

    deleteTodo(id, mainArr, secondArr) {
      const itemIndex = this[mainArr].findIndex(item => item.id === id)

      if (itemIndex !== -1) {
        this[secondArr].push(this[mainArr][itemIndex])
      }

      this[mainArr] = this[mainArr].filter((task) => id !== task.id);
    },

    updateTask({description, id}) {
      this.taskList = this.taskList.map((task) => {
        if(task.id === id) {
          task.taskDescription = description
        }
        return task
      });
    },

    changeActiveTab(newTab) {
      this.isActiveTaskListTab = newTab;
    }
  }
}

</script>

<style>
.todo-app {
  text-align: center;
  margin: 0 auto;
}

</style>
