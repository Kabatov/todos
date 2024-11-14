<template>
    <li class="todo-item">
        <input
            class="todo-item__input-task"
            name="Глядеть"
            v-model="description"
        >
        <button
            class="todo-item__add-button"
            @click="todoDeleteItem"
        >
            Выполненно
        </button>
        <button
            class="todo-item__delete-button"
            @click="todoDeleteItem"
        >
            Не выполненно
        </button>
        <div>
            <span>Приоритет:</span>
            <p class="todo-item__priority-status">{{ priorityStatus }}</p>
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
        taskDescription: {
            type: String,
            required: true
        },
        priorityStatus: {
            type: String,
            required: true
        },
    },

    data() {
        return {
            description: this.taskDescription,
        }
    },

    watch: {
        description(newDes) {
            this.$emit('update-task', {
                description: newDes,
                id: this.id
            })
        }
    },

    methods: {
        todoDeleteItem() {
            this.$emit('delete', this.id);
        }
    }

}
</script>

<style>
.todo-item {
    display: flex;
    justify-content: space-around;
    padding-bottom: 15px;
}

.todo-item__input-task {
  outline: none;
  border: none;
  border: solid 0 #f2f2f2;
  width: 300px;
  font-size: 16px;
}

.todo-item__add-button {
    border: 1px solid black;
    border-radius: 10px;
    background-color: cornflowerblue;
    width: 100px;
    height: 50px;
    font-size: 14px;
}

.todo-item__delete-button {
    border: 1px solid black;
    border-radius: 10px;
    background-color: red;
    width: 100px;
    height: 50px;
    font-size: 14px;
}
</style>
