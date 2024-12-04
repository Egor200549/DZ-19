<script>
import Item from './Item.vue';

let id = 0;

export default {
    data() {
        return {
            todos: []
        }
    },
    components: {
        Item
    },
    methods: {
        addTodo(e) {
            this.todos.unshift({
                id: id++,
                content: e.target.value,
                status: false
            });
            e.target.value = '';
        },
        deleteTodo(id) {
            this.todos.splice(this.todos.findIndex((todo) => id === todo.id), 1);
        },
        performTodo(id) {
            const todo = this.todos.find(todo => todo.id === id);
            if (todo) {
                todo.status = true;
            }
        }
    },
    computed: {
        renderTodos() {
            return this.todos;
        }
    }
}
</script>

<template>
    <section class="real-app">
        <input v-on:keyup.enter="addTodo" class="add-input" type="text">
        <p>для добавления задачи нажмите Enter</p>
        <Item v-on:perform="performTodo" v-on:del="deleteTodo" v-for="todo in renderTodos" :key="todo.id"
            :todo="todo" />
    </section>
</template>

<style scoped>
.real-app {
    padding: 20px;
    width: 600px;
    margin: 0 auto;
    box-shadow: 0 0 5px #666;
}

.add-input {
    outline: 0;
    background-color: inherit;
    border: none;
    font-size: 20px;
    border-bottom: 1px solid white;
    color: white;
    padding: 20px;
    width: 400px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px;
    margin-bottom: 5px;
}
</style>