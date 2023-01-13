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
      <h1>Online Movie Search</h1>
      <div class="form__top">
        <input
          v-model="title"
          type="text"
          placeholder="Search"
          class="form__input form__search"
          name="title"
        />
      </div>
      <div class="form__bottom">
        <label for="year" class="form__label">Year:</label>
        <input
          v-model="year"
          type="text"
          placeholder="Type here"
          class="form__input"
          name="year"
        />
        <label for="type" class="form__label">Type:</label>
        <input
          v-model="type"
          type="text"
          placeholder="Type here"
          class="form__input"
          name="type"
        />
      </div>
    </div>
  </div>
  <div class="main">
    <div class="wrapper">
      <div class="cards__list">
        <p v-if="!Data">Loading...</p>
        <div v-for="card in Data.Search" class="card">
          {{ card }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  margin: 0 auto;
  width: 1024px;
  background-color: rgb(231, 230, 228);
}

.form {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  min-height: 100px;
  font-size: 17px;
  align-items: center;
  width: 800px;
}
.form__top {
  margin-bottom: 10px;
}
.form__bottom {
  display: flex;

  margin-bottom: 30px;
}
.form__search {
  width: 450px;
}
.form__label {
  margin-right: 10px;
}
.form__input {
  height: 30px;
  margin-right: 10px;
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
