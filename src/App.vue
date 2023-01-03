<script setup>
import { ref, watch } from "vue";

const todoId = ref(1);
const todoData = ref(null);

async function fetchData() {
  todoData.value = null;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  );
  todoData.value = await res.json();
}

fetchData();

watch(todoId, fetchData);
</script>

<template>
  <div class="wrapper">
    <div class="form">123</div>
  </div>

  <div class="wrapper">
    <div class="card">
      <p>Todo id: {{ todoId }}</p>
      <button @click="todoId++">Fetch next todo</button>
      <p v-if="!todoData">Loading...</p>
      <pre v-else>{{ todoData }}</pre>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  margin: 0 auto;
  width: 1024px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  background-color: antiquewhite;
}

.form {
  width: 100%;
  min-height: 200px;
  font-size: 12px;
  text-align: center;
  background: rgb(206, 206, 206);
}

.card {
  min-width: 200px;
  min-height: 200px;
  border: 1px solid black;
  margin-right: 20px;
}
</style>
