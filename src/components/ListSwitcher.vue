<template>
  <div class="list-switcher">
    <button
      class="list-switcher__button-left"
      @click="setSelectTask('task-list')"
    >
      Невыполненные задачи
    </button>
    <button
      class="list-switcher__button-right"
      @click="setSelectTask('task-list-completed')"
    >
      Выполненные задачи
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    setSelectTask(str) {
      this.$emit('change-active-tab', str)
    }
  }
}
</script>

<style>
.list-switcher {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  padding: 20px 0 20px 0;
}

.list-switcher__button-left {
  padding: 10px;
  border: 1px solid black;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
  background-color: #afe01c;
  font-size: 15px;
  cursor: pointer;
}

.list-switcher__button-right {
  padding: 10px;
  border: 1px solid black;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  background-color: #afe01c;
  font-size: 15px;
  cursor: pointer;
}
</style>
