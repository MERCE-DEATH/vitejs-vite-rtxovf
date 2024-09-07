<!-- JS -->
<script setup>
import { ref } from 'vue';
/**
todo item {
  text: string
  done : boolean
}
 */
const inputValue = ref('');
const todoList = ref([
  { text: 'vue', done: false },
  { text: 'react', done: false },
  { text: 'vercel', done: false },
]);

console.log(inputValue.value);
const printInputValue = () => {
  console.log(inputValue.value);
};

const handleClickButton = () => {
  const text = inputValue.value;

  todoList.value.push({
    text: text,
    done: false,
  });
};

const handleChange = (event) => {
  const nextValue = event.target.value;
  inputValue.value = nextValue;
};

const handleClickDeleteButton = (index) => {
  todoList.value.slice(index, 1);
};
</script>

<!-- html -->
<template>
  <h4>TODO LIST</h4>
  <p>{{ todoList }}</p>

  <!-- <input v-model="inputValue"/> -->
  <input v-model="inputValue" @change="handleChange" />
  <button @click="handleClickButton">확인</button>

  <div class="todo-item" v-for="(item, idx) in todoList">
    <input type="checkbox" v-model="item.done" />
    <span :class="{ 'done-item': item.done }">
      {{ item.text }}
    </span>

    <div>
      <button>수정</button>
      <button @click="handleClickDeleteButton(idx)">삭제</button>
    </div>
  </div>
</template>

<!-- css -->
<style scoped>
.todo-item {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid gray;
}

.done-item {
  text-decoration: line-through;
}
</style>