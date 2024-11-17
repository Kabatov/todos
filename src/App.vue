<template>
  <div class="todo-app">
    <TodoTitle />
    <TodoAddTask @add-task="addTask"/>
    <TaskListSwitching @set-selected-task-list="setSelectTaskList"/>
    <keep-alive>
      <TodoList
        v-if="activeTaskList === 'task-list'"
        :task-list="taskList"
        @delete-todo="(id) => deleteTodo(id, 'taskList', 'taskListCompleted')"
        :title="'Невыполненные Задачи'"
        @update-task="updateTask"
      />
    </keep-alive>
    <keep-alive>
      <TodoList
        v-if="activeTaskList === 'task-list-completed'"
        :task-list="taskListCompleted"
        @delete-todo="(id) => deleteTodo(id, 'taskListCompleted', 'taskList')"
        :title="'Выполненные Задачи'"
      />
    </keep-alive>
  </div>
</template>

<script>
import TodoAddTask from './components/TodoAddTask.vue';
import TodoList from './components/TodoList.vue';
import TodoTitle from './components/TodoTitle.vue';
import TaskListSwitching from './components/TaskListSwitching.vue';

export default {
  components: {
    TodoTitle,
    TodoList,
    TodoAddTask,
    TaskListSwitching
  },

  data() {
    return {
      taskList: [],
      taskListCompleted: [],
      activeTaskList: 'task-list'
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

    setSelectTaskList(arr) {
      this.activeTaskList = arr;
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
