<template>
  <div class="todo-app">
    <TodoTitle />
    <TodoAddTask @add-task="addTask"/>
    <ListSwitcher @set-selected-task-list="setSelectTaskList"/>
    <keep-alive>
      <div>
        <TodoList
          v-if="activeTab === 'task-list'"
          :task-list="taskList"
          @delete-todo="(id) => deleteTodo(id, 'taskList', 'taskListCompleted')"
          :title="'Невыполненные Задачи'"
          @update-task="updateTask"
        />
        <TodoList
          v-if="activeTab === 'task-list-completed'"
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
      activeTab: 'task-list'
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

    setSelectTaskList(str) {
      this.activeTab = str;
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
