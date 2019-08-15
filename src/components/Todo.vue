<template>
    <div>
        <h1>{{name}}</h1>
        <input type="text" v-model="value">
        <button @click="makeTodo">Make a Todo</button>
        <ul v-for="(todo, index) in todos" class="list-group">
        <div class="col-6">
                <li class="list-group-item">
                    {{todo}}
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
                    id: new Date().getUTCMilliseconds(),
                    value: this.value
                }
                this.todos.push(dataObj)
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