<template>
  <TodoHeader :appTitle="title"></TodoHeader>
  <TodoInput @add="addTodoItem"></TodoInput>
  <TodoList :todoItems="todoItems" @remove="removeTodoItem"></TodoList>
</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue';
import TodoInput from '@/components/TodoInput.vue';
import TodoList from '@/components/TodoList.vue';
import { onBeforeMount, onMounted, onUnmounted, ref } from 'vue';


export default {
  components: {
    TodoHeader,
    TodoInput,
    TodoList
  },
  data() {
    return {
      title: '할일 앱'
    };
  },
  setup() {
    // data
    const todoItems = ref([]);

    // methods
    function fetchTodos() {
      const result = [];
      for(let i = 0; i < localStorage.length; i++) {
          const todoItem = localStorage.key(i);
          result.push(todoItem);
      }
      return result;
    }

    console.log('setup called');

    onBeforeMount(() => {
      console.log('onBeforeMounted called');
      todoItems.value = fetchTodos();
    });

    onMounted(() => {
      console.log('onMounted called');
    });

    onUnmounted(() => {
      console.log('onUnmounted called');
    });

    function addTodoItem(todo) {
      todoItems.value.push(todo);
      localStorage.setItem(todo, todo);
    }
    function removeTodoItem(item, index) {
      todoItems.value.splice(index, 1);
      localStorage.removeItem(item);
    }
    return { todoItems, addTodoItem, removeTodoItem };
  }
}
</script>

<style scoped>

</style>