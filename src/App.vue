<script setup>
import Cards from './components/Cards.vue';
import Forms from './components/Forms.vue';
</script>

<template>
  <div class="formContainer">
    <Forms/>
  </div>
  <div class="formContainer">
    <h3>Data :</h3>
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
}
</style>
