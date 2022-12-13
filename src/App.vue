<template>
  <HeaderTag />
  <AddTodo @clickHandler="clickHandler" :todos="todos" />
  <TodoList :todos="todos" @deleteTodo="deleteTodo" />
</template>

<script>
import HeaderTag from './components/HeaderTag.vue'
import AddTodo from './components/AddTodo.vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    HeaderTag,
    AddTodo,
    TodoList
  },
  data() {
    return {
      todos: [],
      todo: {
        name: ''
      }

    }
  },
  methods: {
    async clickHandler(todo) {

      const res = await fetch('http://localhost:3000/todos', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },

        body: JSON.stringify(todo)

      });

      const data = await res.json();

      this.todos = [...this.todos, data]
    },

    async deleteTodo(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`http://localhost:3000/todos/${id}`, {
          method: 'DELETE',
        })
        res.status === 200 ? (this.todos = this.todos.filter((todo) => todo.id !== id)
        ) : alert('Error deleting todo')
      }
    },

    async fetchDeleteTodos(id) {
      const res = await fetch(`http://localhost:3000/todos/${id}`);

      const data = await res.json();

      return data;
    },

    async fetchTodos() {
      const res = await fetch("http://localhost:3000/todos");

      const data = await res.json();

      return data;
    }
  },

  async created() {
    this.todos = await this.fetchTodos()
  }
}


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
