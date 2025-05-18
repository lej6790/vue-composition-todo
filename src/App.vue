<template>
  <TodoHeader :appTitle="title"></TodoHeader>
  <TodoInput @add="addTodoItem"></TodoInput>
  <TodoList :todoItems="todoItems" @remove="removeTodoItem"></TodoList>
</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue';
import TodoInput from '@/components/TodoInput.vue';
import TodoList from '@/components/TodoList.vue';
import { useTodo } from '@/hooks/useTodo'
import { onBeforeMount } from 'vue'

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
    const { 
      todoItems,
      fetchTodos, 
      addTodoItem, 
      removeTodoItem 
    } = useTodo();

    onBeforeMount(() => {
      // console.log('onBeforeMounted called');
      todoItems.value = fetchTodos();
    });

    return { todoItems, addTodoItem, removeTodoItem };
  }
}
</script>

<style scoped>

</style>