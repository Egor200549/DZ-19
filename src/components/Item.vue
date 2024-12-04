<script>
export default {
    props: {
        todo: {
            type: Object
        }
    },
    methods: {
        deleteTodo() {
            this.$emit('del', this.todo.id);
        },
        performTodo() {
            this.$emit('perform', this.todo.id);
        }
    }
}
</script>

<template>
    <div class="todo-item">
        <div :class="{ 'performed': todo.status }">{{ todo.content }}</div>
        <div>
            <button v-if="!todo.status" v-on:click="performTodo" class="todo-button">Выполнить</button>
            <button v-on:click="deleteTodo" class="todo-button">Удалить</button>
        </div>
    </div>
</template>

<style scoped>
.todo-item {
    position: relative;
    font-size: 24px;
    border-bottom: 1px solid black;
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
    padding: 20px;
    background-color: #ebebeb;
    color: #2d2d2d;
}

.todo-button {
    border: 0;
    border-radius: 4px;
    background-color: black;
    color: #ebebeb;
    padding: 10px 30px;
    cursor: pointer;
}

.todo-button:first-child {
    margin-right: 10px;
}

.performed {
    text-decoration: line-through;
}
</style>