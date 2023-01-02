<script setup>
const getPost = async () => {
  fetch("https://randomuser.me/api/?results=100").then((res) => res.json());
};

console.log(getPost());
</script>

<template>
  <div class="wrapper">
    <div class="form">123</div>
  </div>

  <div class="wrapper">
    <div class="card">123</div>
    <div class="card">123</div>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
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
  border: 1px solid var--color-border;
}
</style>
