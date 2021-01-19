<template>

<div class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans">
	<div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
        <div class="mb-4">
            <h1 class="text-3xl text-left font-bold">Todo List</h1>
            <TodoInput v-on:addTodo="addTodo"></TodoInput>
        </div>
        <div>
            <TodoList :todoItems="todoItemsReverse"></TodoList>
        </div>
    </div>
</div>

</template>

<script>
    import TodoInput from './components/TodoInput.vue';
    import TodoList from './components/TodoList.vue';
    import moment from 'moment'

    export default {
        data() {
            return {
                todoItems: [],
            }
        },
        methods: {
            getTodoItems() {
                const todoItems = localStorage.getItem('todoItems');
                if (todoItems !== null) {
                    this.todoItems = JSON.parse(todoItems);
                }
            },
            addTodo(newTodoItem) {
                console.log(moment().format('MMMM Do YYYY, h:mm:ss a'));
                return;
                if (newTodoItem) {
                    this.todoItems.push({
                        'todo': newTodoItem.trim(),
                        'state': 'ing',
                    });
                    localStorage.setItem('todoItems', JSON.stringify(this.todoItems));
                }
            }
        },
        created() {
            this.getTodoItems();
        },
        computed: {
            todoItemsReverse() {
                return [...this.todoItems].reverse();
            }
        },
        components: {
            'TodoInput': TodoInput,
            'TodoList': TodoList,
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