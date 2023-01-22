<script setup lang="ts">
import { ref, watchEffect } from "vue";

const form = ref({
  search: null,
  year: null,
  type: null,
  page: null,
});
const data: any = ref("");

async function submit() {
  const res = await fetch(
    `http://www.omdbapi.com/?s=${form.value.search}&y=${form.value.year}&page=${form.value.page}&apikey=77b8e5a8`
  );
  data.value = await res.json();
}
</script>

<template>
  <div class="header">
    <h1 class="header__title">Online Movie Search</h1>
    <div class="form">
      <div class="form__search">
        <input
          v-model="form.search"
          type="text"
          placeholder="Search"
          id="form__title"
        />
      </div>
      <div class="form__options">
        <div>
          <label for="form__year" class="form__label">Year</label>
          <input
            v-model="form.year"
            type="text"
            placeholder="Type here"
            id="form__year"
          />
        </div>
        <div>
          <label for="form__type" class="form__label">Type</label>
          <input
            v-model="form.type"
            type="text"
            placeholder="Type here"
            id="form__type"
          />
        </div>
      </div>
    </div>

    <button @click="submit">search</button>
  </div>

  <div class="main">
    <div class="cards__list">
      <p v-if="!data">Loading...</p>
      <div v-for="card in data.Search" class="card">
        {{ card }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.header {
  padding: 10px;
  margin: 0 auto;
  max-width: 1024px;
  background: rgb(207, 198, 187);
}
.header__title {
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
  font-size: 17px;
  max-width: 500px;
}

.form__search {
  margin-bottom: 10px;
  width: 100%;
}

.form input[type="text"] {
  width: 100%;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.form__options {
  display: flex;
  flex-direction: row;
  width: 100%;
  gap: 10px;
  margin-bottom: 20px;
}
.form__options div {
  display: flex;
  flex-direction: column;
  width: 50%;
}

.form__label {
  padding: 0 0 5px 7px;

  display: inline-block;
}
.form__input {
  height: 30px;
}

@media screen and (max-width: 600px) {
  .form__options {
    flex-direction: column;
  }

  .form__options div {
    width: 100%;
  }
}
.main {
  margin: 0 auto;
  width: 1024px;
  background: rgb(243, 243, 243);
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
