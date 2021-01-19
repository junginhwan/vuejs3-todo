<template>
    <div class="flex mb-4 items-center" v-for="(todoItem, index) in todoItems" :key="index">
        <p class="w-full text-left" :class="[ todoItem.state === 'done' ? 'text-green-600 line-through' : 'text-grey-600' ]">{{ todoItem.todo }}</p>
        <button class="flex-none p-2 ml-4 mr-2 border-2 rounded hover:text-white" :class="[ todoItem.state === 'done' ? 'text-gray-500 border-gray-500 hover:bg-gray-500' : 'text-green-600 border-green-600 hover:bg-green-600' ]" @click="changeState(todoItem)">{{ todoItem.state === 'done' ? 'Not Done' : 'Done' }}</button>
        <button class="flex-none p-2 ml-2 border-2 rounded text-red-600 border-red-600 hover:text-white hover:bg-red-600">Remove</button>
    </div>
</template>

<script>
export default {
    props: ['todoItems'],
    methods: {
        changeState(todoItem) {
            console.log(todoItem);
        }
    }
}
</script>
