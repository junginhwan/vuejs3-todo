<template>
 <section>
    <transition-group name="list" tag="div">
        <div class="flex mb-4 items-center border-b-2 border-gray-200 pb-2 border-dotted" v-for="(todoItem, index) in todoItems" :key="index">
            <p class="w-full text-left" :class="[ todoItem.state === 'done' ? 'text-green-600 line-through' : 'text-grey-600' ]">{{ todoItem.todo }}</p>
            <button class="flex-none p-2 ml-4 mr-2 border-2 rounded hover:text-white" :class="[ todoItem.state === 'done' ? 'text-gray-500 border-gray-500 hover:bg-gray-500' : 'text-green-600 border-green-600 hover:bg-green-600' ]" @click="changeState(todoItem, todoItem.state)">{{ todoItem.state === 'done' ? 'Not Done' : 'Done' }}</button>
            <button class="flex-none p-2 ml-2 border-2 rounded text-red-600 border-red-600 hover:text-white hover:bg-red-600 focus:outline-none" @click="deleteTodo(todoItem)">Remove</button>
        </div>
    </transition-group>
  </section>
</template>

<script>
export default {
    props: ['todoItems'],
    methods: {
        changeState(todoItem, state) {
            this.$emit('changeState', todoItem, state === 'ing' ? 'done' : 'ing');
        },
        deleteTodo(todoItem) {
            this.$emit('deleteTodo', todoItem);
        }
    }
}
</script>

<style scoped>
  .list-enter-active, .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }

</style>