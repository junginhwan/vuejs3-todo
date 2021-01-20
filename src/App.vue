<template>

<div class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans">
	<div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
        <div class="mb-4">
            <h1 class="text-3xl text-left font-bold">Todo List</h1>
            <TodoInput v-on:addTodo="addTodo"></TodoInput>
        </div>
        <div>
            <TodoList :todoItems="todoItemsReverse" v-on:changeState="changeState" v-on:deleteTodo="deleteTodo"></TodoList>
        </div>
    </div>
</div>

</template>

<script>
    import TodoInput from './components/TodoInput.vue';
    import TodoList from './components/TodoList.vue';
    import moment from 'moment'
    import { v1 as uuidv1 } from 'uuid';

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
                if (newTodoItem) {
                    this.todoItems.push({
                        todo: newTodoItem.trim(),
                        state: 'ing',
                        date: moment().format('YYYYMMDDHmmss'),
                        id: uuidv1(),
                    });
                    this.storageSave(this.todoItems);
                }
            },
            changeState(todoItem, state) {
                this.todoItems.map((item) => {
                    if (todoItem.id === item.id) {
                        item.state = state;
                    } 
                });
                this.storageSave(this.todoItems);
            },
            storageSave(todoItems) {
                localStorage.setItem('todoItems', JSON.stringify(todoItems));
            },
            deleteTodo(todoItem) {
                const newTodoItem = this.todoItems.filter((item, index) => {
                    return item.id !== todoItem.id
                });
                this.setTodoItems(newTodoItem);
                this.storageSave(newTodoItem);
            },
            setTodoItems(todoItems) {
                this.todoItems = todoItems;
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