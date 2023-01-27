<script setup lang="ts">
const props = defineProps({
  data: Object,
});
</script>

<template>
  <div class="cards__list">
    <div v-for="card in data" class="card">
      <img :src="card.Poster" :alt="card.Title" />
      <h3 class="card__title">{{ card.Title }}</h3>
    </div>
  </div>
</template>

<style scoped>
.cards__list {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
.card {
  width: 190px;
  border: 1px solid black;
  margin: 5px;
  word-wrap: break-word;
}

.card__title {
  color: rgb(148, 47, 69);
}
.card img {
  width: 100%;
  height: auto;
}
</style>
