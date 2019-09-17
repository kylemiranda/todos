<template>
    <div>
        <h1 class="text-center">{{name}}</h1>
        <div class="newTodo" style="text-align: center">
            <input type="text" v-model="value" placeholder="New Todo">
            <button @click="makeTodo">Add Todo</button>
        </div>
        <ul v-for="(todo, index) in todos" class="list-group">
            <div class="row justify-content-center">
                <li class="list-group-item" style="max-width: 400px; text-align: center">
                    {{todo.value}}
                    <button class="btn btn-primary" @click="moveTodo(index, 'down')">Down</button>
                    <button class="btn btn-primary" @click="moveTodo(index)">Up</button>
                    <button class="btn btn-danger" @click="deleteTodo(index)">X</button>
                </li>
            </div>
        </ul>
    </div>
</template>

<style lang="css">

</style>

<script>
    export default {
        name: 'Todo',
        props: {
            name: String
        },
        data: function () {
            return {
                todos: [],
                value: ''
            }
        },
        methods: {
            makeTodo: function () {
                var dataObj = {
                    //id: new Date().getUTCMilliseconds(),
                    value: this.value
                }
                this.todos.push(dataObj)
                this.value = ''
            },
            deleteTodo: function (index) {
                this.todos.splice(index, 1);
            },
            moveTodo: function (index, dir) {
                if (dir === 'down') {
                    var newIndex = index + 1;
                    if (newIndex >= this.todos.length) {
                        newIndex = 0;
                    }
                    this.todos.splice(newIndex, 0, this.todos.splice(index, 1)[0])
                } else {
                    var newIndex = index - 1;
                    if (newIndex === -1) {
                        newIndex = this.todos.length + 1;
                    }
                    this.todos.splice(newIndex, 0, this.todos.splice(index, 1)[0])
                }
            }
        }
    }
</script>