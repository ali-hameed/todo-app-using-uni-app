<script setup>
import { onMounted, ref, reactive } from 'vue';
import AddNewTodo from '../../components/AddNewTodo.vue';
import TodoList from '../../components/TodoList.vue';
import { uuidv4 } from '../../utils';

const appTitle = ref('تطبيق قائمة المهام');
const todos = reactive([]);

// add new todo method
const addTodo = (todoText) => {
  if (!todoText) {
    return my.alert({
      title: 'تنبيه',
      content: 'يجب  ملء حقل المهمة الجديدة',
      buttonText: 'حسناً',
    });
  }
  todos.push({
    id: uuidv4(),
    text: todoText,
    done: false,
  });
};

// toggle the done state in each clicked todo
const toggleDone = (id) => {
  todos.forEach((item) => {
    if (item.id === id) {
      item.done = !item.done;
    }
  });
};

// delete todo by id method
const deleteTodo = (id) => {
  const index = todos.findIndex((item) => item.id === id);
  if (index !== -1) {
    todos.splice(index, 1);
  }
};

onMounted(() => {
  uni.loadFontFace({
    family: 'IBM Plex Sans Arabic',
    source: "url('../../static/fonts/IBMPlexSansArabic-Regular.ttf')",
  });
});
</script>

<template>
  <view class="container arabic-font dir-rtl">
    <view class="title">
      {{ appTitle }}
    </view>
    <AddNewTodo v-on:add-new-todo="addTodo" />
    <TodoList
      :todos="todos"
      v-on:toggle-done="toggleDone"
      v-on:delete-todo="deleteTodo"
    />
  </view>
</template>

<style scoped>
.dir-rtl {
  direction: rtl;
}

.container {
  margin: 0 20px;
}
.arabic-font {
  font-family: 'IBM Plex Sans Arabic', sans-serif;
  font-weight: normal;
}

.title {
  font-size: 30px;
  color: white;
  margin-top: 10px;
  margin-bottom: 20px;
}

.content {
  font-size: 20px;
  color: white;
}
</style>
