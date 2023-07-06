<script setup lang="ts">
const props = defineProps({
  data: Object,
});
</script>

<template>
  <v-container>
    <v-row>
      <v-col
        v-for="card in data"
        :key="card"
        cols="12"
        xs="12"
        sm="6"
        md="4"
        lg="3"
      >
        <v-card :title="card.Title">
          <img :src="card.Poster" class="card__img" :alt="card.Title"
        /></v-card>
      </v-col>
    </v-row>
  </v-container>
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
