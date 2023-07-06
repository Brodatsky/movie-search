<script setup lang="ts">
import { ref, watch } from "vue";
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
  let res: any = await fetch(
    `https://www.omdbapi.com/?s=${form.value.search}&y=${form.value.year}&type=${form.value.type}&page=${form.value.page}&apikey=77b8e5a8`
  );

  let obj = await res.json();
  data.value = obj.Search;
  isLoading.value = false;
}

watch(() => form.value.page, getPage);
</script>

<template>
  <v-app>
    <div class="header mb-5 pb-3">
      <h1 class="header__title my-3">Online Movie Search</h1>
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
        <v-btn block @click.prevent="getPage" class="py-6"> Search </v-btn>
      </div>
    </div>
    <v-main>
      <v-overlay v-model="isLoading" class="align-center justify-center">
        <v-progress-circular
          v-if="isLoading"
          :indeterminate="isLoading"
          size="64"
          color="secondary"
          class="mx-auto"
        ></v-progress-circular
      ></v-overlay>
      <div v-if="data" class="d-flex justify-space-around mb-3">
        <v-pagination
          v-model="form.page"
          :length="10"
          :total-visible="5"
          rounded="circle"
        ></v-pagination>
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
  margin: 0 auto;
  width: 100%;
  background: rgb(117, 215, 228);
}
.header__title {
  font-weight: bold;
  text-align: center;
  font-family: "Lobster", sans-serif;
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

.main {
  margin: 0 auto;
  width: 1024px;
  background: rgb(243, 243, 243);
}
</style>
