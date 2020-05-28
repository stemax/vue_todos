<template>
    <form @submit.prevent="onsubmit">
        <b-input-group prepend="TODO:" class="mt-3">
            <b-form-input v-model="title" type="text"></b-form-input>
            <b-input-group-append>
                <b-button variant="primary" type="submit">Add</b-button>
            </b-input-group-append>
        </b-input-group>
    </form>
</template>

<script>
    export default {
        name: "AddTodo",
        data() {
            return {
                title: ''
            }
        },
        methods: {
            onsubmit(){
                //console.log('Submited ', this.title)
                if (this.title.trim()) {
                    const newTodo = {
                        id: Date.now(),
                        title: this.title,
                        completed: false
                    }
                    this.$emit('add-todo', newTodo)
                    this.title = '';
                }
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
    }
</style>
