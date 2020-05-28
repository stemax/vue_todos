<template>
    <div>
        <b-progress v-bind:progress="countAndProgress" :value="progress" :max="max"
                    variant="success" show-progress height="2rem"/>
        <AddTodo @add-todo="addTodo"/>
        <b-button-group v-if="!loading" class="mt-3">
            <b-button variant="primary" @click="setFilter('all')">
                All:
                <b-badge variant="light">{{total}}</b-badge>
            </b-button>
            <b-button variant="success" @click="setFilter('completed')">
                Completed:
                <b-badge variant="light">{{completed}}</b-badge>
            </b-button>
            <b-button variant="warning" @click="setFilter('not-completed')">
                Not Completed:
                <b-badge variant="light" >{{not_completed}}</b-badge>
            </b-button>
        </b-button-group>
        <b-input-group prepend="Show" class="mt-3">
            <b-form-select v-if="!loading" v-model="filter" :options="options"></b-form-select>
        </b-input-group>

        <Loader v-if="loading"/>

        <TodoList
                v-else-if="filteredTodos.length"
                v-bind:todos="filteredTodos"
                @remove-todo="removeTodo"/>
        <p v-if="!loading&&!todos.length">No todos!</p>
    </div>
</template>

<script>
    import TodoList from "@/components/TodoList";
    import AddTodo from "@/components/AddTodo";
    import Loader from "@/components/Loader";

    export default {
        name: 'App',
        data() {
            return {
                /*                todos: [
                                    {id: 1, title: 'Приготовить завтрак', completed: false},
                                    {id: 2, title: 'Сходить в магазин', completed: true},
                                    {id: 3, title: 'Прочитать книгу', completed: false},
                                ],*/
                todos: [],
                loading: true,
                filter: 'all',
                progress: 0,
                max: 100,
                options: [
                    {value: 'all', text: 'All'},
                    {value: 'completed', text: 'Completed'},
                    {value: 'not-completed', text: 'Not Completed'},
                ],
                completed: 0,
                not_completed: 0,
                total: 0,
            }
        },
        /*        watch:{
                    filter(value){
                        console.log(value)
                    }
                },*/
        computed: {
            filteredTodos() {
                let result = this.todos;
                if (this.filter === 'all') {
                    result = this.todos
                } else if (this.filter === 'completed') {
                    result = this.todos.filter(t => t.completed)
                } else if (this.filter === 'not-completed') {
                    result = this.todos.filter(t => !t.completed)
                }
                return result
            },
            countAndProgress() {
                let todosCount = this.todos.length;
                let todosCompletedCount = this.todos.filter(t => t.completed).length
                this.setTotal(todosCount);
                this.setProgressCompleted(todosCompletedCount);
                this.setProgressNotCompleted(todosCount - todosCompletedCount);
                this.setProgress(todosCompletedCount / todosCount * 100);
                return this.progress
            }
        },
        async mounted() {
            await fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
                .then(response => response.json())
                .then(json => {
                    setTimeout(() => {
                        this.todos = json
                        this.loading = false
                    }, 0)
                })
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter(t => t.id !== id)
            },
            addTodo(todo) {
                this.todos.push(todo)
            },
            setFilter(filter) {
                this.filter = filter
            },
            setTotal(count) {
                this.total = count
            },
            setProgressCompleted(count) {
                this.completed = count
            },
            setProgressNotCompleted(count) {
                this.not_completed = count
            },
            setProgress(count) {
                this.progress = count
            }
        },
        components: {
            AddTodo,
            TodoList,
            Loader
        }
    }
</script>

<style>
    /*
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }*/
</style>
