<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
        </header>
        <div class="main">
            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :key="todo.id" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle">
                        <label>{{ todo.name }}</label>
                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                    </div>
                </li>
            </ul>
        </div>
        <footer class="footer" v-show="todos.length > 0">
            <span class="todo-count"> <strong> {{ remaining }} </strong> tâches à faire </span>
            <ul class="filters">
                <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
                <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a></li>
                <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
            </ul>

            <button class="clear-completed" v-show="completed" @click.prevent="deleteCompleted" >Supprimer les tâches finies</button>
        </footer>
    </section>
</template>

<script>
export default {
    data() {
        return {
            todos: [{
                name: 'tache de test',
                completed: false,
            }],
            newTodo: '',
            filter: 'all'
        }
    },
    methods : {
        addTodo() {
            this.todos.push({
                completed: false,
                name: this.newTodo,

            })
            this.newTodo = ''
        },
        deleteTodo (todo) {
            this.todos= this.todos.filter(i => i !== todo)
        },
        deleteCompleted () {
            this.todos = this.todos.filter(todo => !todo.completed)
        }
    },
    computed: {
            remaining () {
                return this.todos.filter(todo => !todo.completed).length
            },
            completed () {
                return this.todos.filter(todo => todo.completed).length
            },
            filteredTodos () {
                if (this.filter === 'todo') {
                    return this.todos.filter(todo => !todo.completed)
                } else if (this.filter === 'done') {
                    return this.todos.filter(todo => todo.completed)
                }
                return this.todos
            }
        }

    }

</script>

<style src="./todos.css">

</style>