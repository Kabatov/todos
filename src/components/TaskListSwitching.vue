<template>
  <div class="task-list-switching">
    <button
      class="task-list-switching__button"
      @click="setSelectTask('task-list')"
    >
      Невыполненные задачи
    </button>
    <button
      class="task-list-switching__button"
      @click="setSelectTask('task-list-completed')"
    >
      Выполненные задачи
    </button>
  </div>
</template>

<script>
export default {
    props: ['task-list', 'task-list-completed'],

    methods: {
        setSelectTask(arr) {
            this.$emit('set-selected-task-list', arr)
        }
    }
}
</script>

<style>
.task-list-switching {
    width: 600px;
    margin: 0 auto;
    display: flex;
    justify-content: space-around;
    padding: 20px 0 20px 0;
}

.task-list-switching__button {
    padding: 10px;
    border: 1px solid black;
    border-radius: 10px;
    background-color: rgb(175, 224, 28);
    font-size: 15px;
}
</style>
