<script setup>
import { ref, onUpdated, watchEffect } from "vue";
const title = ref("");
const year = ref("");
const page = ref("1");

const emit = defineEmits(["childData"]);

async function submit() {
  let obj = null;
  const res = await fetch(
    `http://www.omdbapi.com/?s=${title.value}&y=${year.value}&page=${page.value}&apikey=77b8e5a8`
  );
  obj = await res.json();
  emit("childData", obj);
}
</script>
<template>
  <div class="form">
    <div class="form__search">
      <input
        v-model="title"
        type="text"
        placeholder="Search"
        id="form__title"
      />
    </div>
    <div class="form__options">
      <div>
        <label for="form__year" class="form__label">Year</label>
        <input
          v-model="year"
          type="text"
          placeholder="Type here"
          id="form__year"
        />
      </div>
      <div>
        <label for="form__type" class="form__label">Type</label>
        <input
          v-model="type"
          type="text"
          placeholder="Type here"
          id="form__type"
        />
      </div>
    </div>
  </div>

  <button @click="submit">emit</button>
</template>
<style scoped>
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
</style>
