<script setup>
import Cards from './components/Cards.vue';
import Forms from './components/Forms.vue';
</script>

<template>
  <h1>Job Application</h1>
  <div class="formContainer">
    <Forms/>
  </div>
  <h2>Applicants</h2>
  <div class="cardsContainer">
    <Cards/>
  </div>
</template>

<style scoped>
.formContainer{
  border: 1px solid rgb(229, 231, 235);
  padding: 2rem;
  border-radius: 1rem;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
  margin-block:2rem;
  width: fit-content;
  max-width: 80vw;
  margin-bottom:5rem;
}
.cardsContainer{
  border: 1px solid rgb(229, 231, 235);
  padding: 2rem;
  border-radius: 1rem;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 80vw;
  margin-bottom:5rem;
}

h1{
  margin-block: 2rem;
}
h2{
  margin-block: 3rem;
  font-size: 2.5rem;
}
</style>
