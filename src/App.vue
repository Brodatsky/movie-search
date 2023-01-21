<script setup>
import Search from "./components/Search.vue";
import { ref } from "vue";

const Data = ref("No child msg yet");
</script>

<template>
  <div class="header">
    <h1 class="header__title">Online Movie Search</h1>
    <Search @childData="(res) => (Data = res)" />
  </div>
  <!-- <p>{{ Data }}</p> -->

  <div class="main">
    <div class="cards__list">
      <p v-if="!Data">Loading...</p>
      <div v-for="card in Data.Search" class="card">
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
