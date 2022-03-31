<template>
  <div class="page_layout">
    <h1>{{ msg }}</h1>
    <div>
      <p v-for="character in data" :key="character.id">
        {{ character.name }}
      </p>
    </div>
    <TheFooter />
  </div>
</template>

<script setup>
import { ref } from "vue";
import TheFooter from "../components/TheFooter.vue";

const data = ref();

async function fetchData() {
  try {
    // fetch data from the api
    const response = await fetch("https://api.disneyapi.dev/characters");
    // If the data isn't 200 return, log error
    if (!response.ok) {
      throw new Error(`Response Error : ${response.status}`);
    }
    // set variable to the json datat of the response
    const responseData = await response.json();

    // add the data to our funtion
    console.log(responseData);
    // set the json datat from the response to the outside data
    data.value = await responseData.data;
  } catch (err) {
    throw new Error(`This is a catch statement error: ${err}`);
  }
}
fetchData();

const msg = "Welcome to the Disney API Character List";
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  display: flex;
  justify-content: center;
  font-size: 40px;
}

p {
  display: flex;
  justify-content: center;
  font-size: 18px;
}
.page_layout {
  margin: 0;
  padding: 0;
}
</style>
