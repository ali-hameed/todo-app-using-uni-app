<script setup>
defineProps(['todo']);

defineEmits(['toggle-done', 'delete-todo']);
</script>

<template>
  <view
    class="todo-item"
    :style="{
      backgroundColor: todo.done ? '#22c55e' : '#14532d',
    }"
  >
    <view
      class="todo-text"
      :style="{
        textDecoration: todo.done ? 'line-through' : '',
      }"
    >
      {{ todo.text }}
    </view>
    <view class="todo-actions">
      <view class="todo-icon" @click="$emit('toggle-done', todo.id)">
        <img
          v-if="todo.done"
          src="../static/icons/undo.png"
          alt="Icon"
          :style="{
            width: 22,
            height: 22,
          }"
        />
        <img
          v-else
          src="../static/icons/tick.png"
          alt="Icon"
          :style="{
            width: 22,
            height: 22,
          }"
        />
      </view>
      <view class="todo-icon" @click="$emit('delete-todo', todo.id)">
        <img
          src="../static/icons/delete.png"
          alt="Icon"
          :style="{
            width: 22,
            height: 22,
          }"
        />
      </view>
    </view>
  </view>
</template>

<style scoped>
.todo-item {
  color: white;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.todo-actions {
  display: flex;
  align-items: center;
  gap: 15px;
}
</style>
