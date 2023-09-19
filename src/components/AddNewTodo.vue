<script setup>
import { ref, reactive, computed } from 'vue';
const msg = ref('أضافة مهمة جديدة');

const showForm = ref(false);
const textInput = ref('');
const placeholders = reactive({
  todoTitle: 'أكتب مهمة جديدة',
});

const showButtonText = computed(() => (showForm.value ? 'أخفاء' : 'أضافة'));

const showButtonColor = computed(() =>
  showForm.value ? '#ef4444' : '#0ea5e9'
);

const toggleShowForm = () => {
  showForm.value = !showForm.value;
};
defineEmits(['add-new-todo']);
</script>

<template>
  <view class="text">
    <view class="new-todo-header">
      <view class="new-todo-title" style="flex: 4">{{ msg }}</view>
      <button
        @click="toggleShowForm"
        class="show-btn rounded-md flex-center"
        :style="{
          flex: 1,
          backgroundColor: showButtonColor,
        }"
      >
        <text>
          {{ showButtonText }}
        </text>
      </button>
    </view>

    <view class="new-todo-input-group" v-if="showForm">
      <input
        style="flex: 3"
        class="add-input font-16 rounded-md"
        type="text"
        name="todoTitle"
        :placeholder="placeholders.todoTitle"
        v-model="textInput"
      />
      <button
        @click="$emit('add-new-todo', textInput)"
        style="flex: 1"
        class="add-btn font-16 rounded-md flex-center"
      >
        <view>أضافة</view>
      </button>
    </view>
  </view>
</template>

<style scoped>
.new-todo-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}
.new-todo-title {
  font-size: 18px;
}
.text {
  color: white;
}

.flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.font-16 {
  font-size: 16px;
}

.rounded-md {
  border-radius: 8px;
}

.new-todo-input-group {
  display: flex;
  align-items: center;
  gap: 8px;
}

.add-input {
  outline: 0;
  border: 0;
  padding: 6px 10px;
}

.add-btn {
  border: 0;
  outline: 0;
  background-color: #0ea5e9;
  color: white;
  height: 38px;
  padding: 0 !important;
}

.show-btn {
  border: 0;
  outline: 0;
  color: white;
  height: 30px;
  font-size: 14px;
}
</style>
