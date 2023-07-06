<script setup lang="ts">
import { ref } from "vue";
import CardList from "./components/CardList.vue";

const form = ref({
  search: "",
  year: "",
  type: "",
  page: 1,
});

const selectItems = ref([
  { title: "All", value: "" },
  { title: "Movie", value: "Movie" },
  { title: "Series", value: "Series" },
]);

const data: any = ref("");
const isLoading = ref(false);

async function getPage() {
  isLoading.value = true;
  console.log(form);

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
  <v-app>
    <div class="header">
      <h1 class="header__title">Online Movie Search</h1>
      <div class="form">
        <v-text-field
          variant="solo-filled"
          v-model="form.search"
          label="Search"
          class="w-100"
          id="form__title"
        ></v-text-field>

        <div class="d-flex justify-space-between w-100">
          <div class="w-50 mr-5">
            <v-text-field
              variant="solo-filled"
              v-model="form.year"
              label="Year"
              type="number"
            ></v-text-field>
          </div>
          <div class="w-50">
            <v-select
              v-model="form.type"
              label="Type"
              :items="selectItems"
              variant="solo"
            ></v-select>
          </div>
        </div>
        <v-btn block @click.prevent="getPage"> Search </v-btn>
      </div>
    </div>
    <v-main>
      <div v-if="data" class="d-flex justify-space-around mb-5">
        <v-btn @click="prevPage">Prev</v-btn>
        <v-progress-circular
          v-if="isLoading"
          :indeterminate="isLoading"
          size="24"
          class="ms-2"
        ></v-progress-circular>
        <v-btn @click="nextPage">Next</v-btn>
      </div>

      <CardList :data="data" />
    </v-main>
  </v-app>
</template>

<style scoped>
.loader {
  position: absolute;
}
.header {
  padding: 10px;
  margin: 0 auto;
  width: 100%;
  background: rgb(117, 215, 228);
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
  background: rgb(173, 170, 170);
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
