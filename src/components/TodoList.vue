<template>
    <ul>
        <li :key="todo.id" v-for="todo in todos">
            <div class="list-container">
                <h3>{{ todo.name }}</h3>
                <button @click="deleteTodo(todo.id)" class="delete-btn">Delete Todo</button>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'TodoList',
    props: {
        todos: Array,
        todo: Object
    },
    methods: {
        deleteTodo(id) {
            this.$emit('deleteTodo', id);
        }
    }
}
</script>

<style scoped>
ul {
    display: flex;
    flex-direction: column;
}

li {
    list-style: none;
}

.list-container {
    display: flex;
    align-items: center;
    justify-content: space-around;
}
</style>