<template>
    <!-- Native not bootstrap code
    <li>
        <span v-bind:class="{done: todo.completed}">

            <b-form-checkbox size="lg"
                             :checked="todo.completed"
                             v-on:change="todo.completed = !todo.completed">
                {{ todo.title | uppercase}}
            </b-form-checkbox>

            <strong>{{index + 1}}</strong>.
            <input type="checkbox" :id="index+1" :checked="todo.completed" v-on:change="todo.completed = !todo.completed">
            <label :for="index+1"> {{ todo.title | uppercase}}</label>

        </span>
        <button class="rm" v-on:click="$emit('remove-todo', todo.id)">
            <b-icon icon="trash"></b-icon>
        </button>
    </li>-->
    <b-list-group-item v-bind:variant="getVariant">
        <b-form-checkbox class="todo-item" size="lg"
                         :checked="todo.completed"
                         v-on:change="todo.completed = !todo.completed"
                         v-bind:class="{done: todo.completed}">
            <del v-if="todo.completed">{{ todo.title | uppercase}}</del>
            <span v-else>{{ todo.title | uppercase}}</span>

        </b-form-checkbox>
        <span style="float: right;cursor: pointer">
                <b-icon icon="trash" v-on:click="$emit('remove-todo', todo.id)"></b-icon>
        </span>
    </b-list-group-item>
</template>

<script>
    export default {
        name: "TodoItem",
        props: {
            todo: {
                type: Object,
                required: true
            },
            index: Number
        },
        filters: {
            uppercase(title) {
                return title.toUpperCase()
            }
        },
        computed: {
            getVariant() {
                return this.todo.completed ? "success" : "";
            }
        }
    }
</script>

<style >

    .todo-item {
        float: left;
      }

    .todo-item label{
        cursor: pointer;
    }

    /*li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
    }

    .rm {
        background: red;
        color: #fff;
        border-radius: 50%;
        font-weight: bold;
        height: fit-content;
        cursor: pointer;
    }
    .done{
        text-decoration: line-through !important;
    }

    input {
        margin-right: 1rem;
    }*/
</style>
