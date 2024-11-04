<template>
    <li class="todo-item">
        <input
            class="todo-input-task"
            type="text"
            name="Пердеть"
            :value=task_description
        >
        <!-- <p class="todo-input-task">{{ task_description }}</p> -->
        <button
            @click="todoDeleteItem"
            :style="uncompletedTaskButtonStyle"
        >
            Выполненно
        </button>
        <button
            @click="todoDeleteItemComplete"
            :style="completedTaskButtonStyle"
        >
            Не выполненно
        </button>
        <div>
            <span>Приоритет:</span>
            <p class="todo-priority-status">{{ priority_status }}</p>
        </div>
    </li>
</template>

<script>
export default {
    data() {
        return {
            uncompletedTaskButtonStyle: {
                border: '1px solid black',
                borderRadius: '10px',
                backgroundColor: 'cornflowerblue',
                width: '100px',
                height: '50px',
                fontSize: '14px'
            },

            completedTaskButtonStyle: {
                border: '1px solid black',
                borderRadius: '10px',
                backgroundColor: 'red',
                width: '100px',
                height: '50px',
                fontSize: '14px'
            },
        }
    },

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
        },

        todoDeleteItemComplete() {
            this.$emit('delete-complete', this.id);
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
</style>
