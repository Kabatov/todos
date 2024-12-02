<template>
    <li class="todo-item">
        <input
            class="todo-item__input-task"
            name="Глядеть"
            v-model="description"
        >
        <select
            class="todo-item__select"
            @change="selectedTaskList"
            :value="isCompleted"
        >
            <option :value="false">Не выполненно</option>
            <option :value="true">Выполненно</option>
        </select>
        <div>
            <span>Приоритет:</span>
            <p class="todo-item__priority-status">{{ priorityStatus }}</p>
        </div>
        <div v-show="this.tagStatus !== null">
            <span>Тег:</span>
            <p class="todo-item__tag-status">{{ tagStatus }}</p>
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
        tagStatus: {
            type: String,
            required: true
        },
        isCompleted: {
            type: Boolean,
            required: false
        }
    },

    data() {
        return {
            description: this.taskDescription
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
        selectedTaskList(event) {
            this.$emit('change-selected-task-list', Boolean(event.target.value), this.id);
            console.log(event.target.value);

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

.todo-item__select {
    border-radius: 10px;
    background-color: cornflowerblue;
    height: 50px;
    font-size: 14px;
}
</style>
