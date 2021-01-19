<template>
    <div class="flex mt-4">
        <input class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker" placeholder="Add Todo" v-model="newTodoItem" @keyup.enter="addTodo">
        <button class="flex-none p-2 border-2 rounded text-green-400 border-green-400 hover:text-white hover:bg-green-400" @click="addTodo">Add</button>
    </div>
</template>

<script>
export default {
    data () {
        return {
            newTodoItem: '',
        }
    },
    methods: {
        addTodo() {
            if (this.newTodoItem) {
                this.$emit('addTodo', this.newTodoItem);
                this.clearInput();
            }
        },
        clearInput() {
            this.newTodoItem = "";
        }
    }
}
</script>