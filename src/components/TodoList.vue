<script setup>
import Todo from './Todo.vue';

defineProps({
  todos: Object,
});

defineEmits(['toggle-done', 'delete-todo']);
</script>

<template>
  <view class="todo-list">
    <view v-if="todos.length > 0">
      <Todo
        v-for="(todo, index) in todos"
        :todo="todo"
        :key="index"
        v-on:toggle-done="(id) => $emit('toggle-done', id)"
        v-on:delete-todo="(id) => $emit('delete-todo', id)"
      />
    </view>
    <view class="no-todos" v-else>{{ 'لا يوجد مهام' }}</view>
  </view>
</template>

<style scoped>
.todo-list {
  margin-top: 15px;
  margin-bottom: 30px;
}

.no-todos {
  color: white;
  font-size: 20px;
  text-align: center;
  padding-top: 20px;
}
</style>
