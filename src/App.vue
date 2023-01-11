<script setup>
import { ref, watchEffect } from "vue";

const title = ref("");
const year = ref("");
const Data = ref(null);

watchEffect(async () => {
  Data.value = null;
  const res = await fetch(
    `http://www.omdbapi.com/?t=${title.value}&y=${year.value}&apikey=77b8e5a8`
  );
  Data.value = await res.json();
});
</script>

<template>
  <div class="wrapper">
    <div class="form">
      <p>Title: {{ title }}</p>
      <input v-model="title" placeholder="Type here" />
      <p>Year: {{ year }}</p>
      <input v-model="year" placeholder="Type here" />
    </div>
  </div>

  <div class="wrapper">
    <div class="card">
      <p v-if="!Data">Loading...</p>
      <pre v-else>{{ Data }}</pre>
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
