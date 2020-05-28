<template>
    <div>
        <!-- Native not bootstrap code
        <ul>
            <TodoItem
                    v-for="(todo, i) of todos" :key="todo.id"
                    v-bind:todo="todo"
                    v-bind:index="i"
                    @remove-todo="removeTodo"
            />
        </ul>-->
        <b-list-group>
            <TodoItem
                    v-for="(todo, i) of todos" :key="todo.id"
                    v-bind:todo="todo"
                    v-bind:index="i"
                    @remove-todo="removeTodo"
            />
        </b-list-group>
    </div>
</template>

<script>
    import TodoItem from "@/components/TodoItem";
    export default {
        name: "TodoList",
        props:['todos'],
        components: {
            TodoItem
        },
        methods: {
            removeTodo(id) {
                this.$emit('remove-todo', id);
            }
        }
    }
</script>

<style scoped>
    ul{
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>
