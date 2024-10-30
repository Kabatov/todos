<template>
    <li class="todo-item">
        <input class="todo-input-task" type="text" name="Пердеть" :value=task_description>
        <!-- <p class="todo-input-task">{{ task_description }}</p> -->
        <button @click="todoDeleteItem" class="todo-delete-button">Сделано</button>
        <div>
            <span>Приоритет:</span>
            <p class="todo-priority-status">{{ priority_status }}</p>
        </div>
    </li>
</template>

<script>
export default {
    props: {
        id: {
            type: Number,
            required: true
        },
        task_description: {
            type: String,
            required: true
        },
        priority_status: {
            type: String,
            required: true
        },
    },

    methods: {
        todoDeleteItem() {
            this.$emit('delete', this.id);
        }
    }

}
</script>

<style>
.todo-input-task {
  outline: none;
  border: none;
  border: solid 0 #f2f2f2;
  width: 300px;
  font-size: 16px;
}

.todo-item {
    display: flex;
    justify-content: space-around;
    padding-bottom: 15px;
}

.todo-delete-button {
    border: 1px solid black;
    border-radius: 10px;
    background-color: cornflowerblue;
    width: 80px;
    height: 50px;
    font-size: 14px;
}
</style>
