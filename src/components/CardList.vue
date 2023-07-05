<script setup lang="ts">
const props = defineProps({
  data: Object,
});
</script>

<template>
  <div class="cards__list">
    <div v-for="card in data">
      <v-sheet :title="card.Title" class="card">
        <img :src="card.Poster" class="card__img" :alt="card.Title"
      /></v-sheet>
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
  background: rgb(255, 255, 255);
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
