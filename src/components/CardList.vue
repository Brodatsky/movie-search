<script setup lang="ts">
const props = defineProps({
  data: Object,
});
</script>

<template>
  <div class="cards__list">
    <div v-for="card in data" class="card">
      <img :src="card.Poster" class="card__img" :alt="card.Title" />

      <h3 class="card__title">{{ card.Title }}</h3>
    </div>
  </div>
</template>

<style scoped>
.cards__list {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 20px;
}
.card {
  padding: 5px;
  width: 190px;
  border: 1px solid black;
  background: rgb(212, 212, 212);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.card__title {
  color: rgb(0, 0, 0);
  text-align: center;
  word-wrap: break-word;
}

.card__img {
  width: 100%;
}
</style>
