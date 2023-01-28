<script setup lang="ts">
import { ref } from "vue";
import CardList from "./components/CardList.vue";

const form = ref({
  search: "",
  year: "",
  type: "",
  page: 1,
});

const data: any = ref("");
const isLoading = ref(false);

async function getPage() {
  isLoading.value = true;
  let res: any = await fetch(
    `https://www.omdbapi.com/?s=${form.value.search}&y=${form.value.year}&type=${form.value.type}&page=${form.value.page}&apikey=77b8e5a8`
  );
  let obj = await res.json();
  data.value = obj.Search;

  isLoading.value = false;
}

function nextPage() {
  form.value.page++;
  getPage();
}

function prevPage() {
  form.value.page < 2 ? form.value.page : form.value.page--;
  getPage();
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
          class="form__option"
        />
      </div>
      <div class="form__options">
        <div>
          <label for="form__year" class="form__label">Year</label>

          <input
            v-model="form.year"
            id="form__year"
            type="number"
            min="1900"
            max="2023"
            step="1"
            class="form__option"
          />
        </div>
        <div>
          <label for="form__type" class="form__label">Type</label>

          <select v-model="form.type" id="form__type" class="form__option">
            <option>Movie</option>
            <option>Series</option>
            <option value="" selected>All</option>
          </select>
        </div>
      </div>

      <button @click="getPage" class="btn">Search</button>
    </div>
  </div>

  <div class="main">
    <CardList :data="data" />

    <div v-if="data" class="main__btns">
      <button @click="prevPage" class="btn">Prev</button>
      <p class="loader" v-if="isLoading">Loading...</p>
      <button @click="nextPage" class="btn">Next</button>
    </div>
  </div>
</template>

<style scoped>
.loader {
  position: absolute;
}
.header {
  padding: 10px;
  margin: 0 auto;
  max-width: 1024px;
  background: rgb(204, 204, 204);
  margin-bottom: 20px;
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
  margin-bottom: 20px;
  font-size: 17px;
  max-width: 500px;
}

.form__search {
  margin-bottom: 10px;
  width: 100%;
}

.form__option {
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
  margin-bottom: 30px;
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

.main__btns {
  display: flex;
  justify-content: space-around;
}
.btn {
  background: rgb(102, 109, 102);
  color: rgb(255, 255, 255);
  width: 30%;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
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
</style>
