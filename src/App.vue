<script setup>
import { ref, watchEffect, onMounted, onUpdated } from "vue";

const title = ref("");
const year = ref("");
const page = ref("1");
const Data = ref(null);

watchEffect(async () => {
  try {
    Data.value = null;
    const res = await fetch(
      `http://www.omdbapi.com/?s=${title.value}&y=${year.value}&page=${page.value}&apikey=77b8e5a8`
    );
    Data.value = await res.json();
  } catch (error) {
    console.log(error);
  }
});

onUpdated(() => {
  console.log(Data.value);
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
    <div class="cards__list">
      <p v-if="!Data">Loading...</p>
      <div v-for="card in Data.Search" class="card">
        {{ card }}
      </div>
      <!-- <pre v-else>{{ Data.Search }}</pre> -->
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  margin: 0 auto;
  width: 1024px;
  display: flex;
  justify-content: center;
  background-color: antiquewhite;
}

.form {
  width: 100%;
  min-height: 100px;
  font-size: 12px;
  text-align: center;
  background: rgb(206, 206, 206);
}

.card {
  width: 190px;
  border: 1px solid black;
  margin: 5px;
  word-wrap: break-word;
}
.cards__list {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
