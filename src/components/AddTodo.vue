<template>
    <div>
        <input type="text" v-model="todo" placeholder="Todo">
        <input type="submit" @click="clickHandler" value="Add Todo" class="add-btn">
    </div>
</template>

<script>

export default {
    name: 'AddTodo',
    data() {
        return {
            todo: ''
        }
    },
    methods: {
        clickHandler() {
            const newTodo = {
                name: this.todo,
            }

            this.$emit('clickHandler', newTodo);
            this.todo = ''
        }
    },

}
</script>