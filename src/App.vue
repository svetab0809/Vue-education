<script setup>

import ReviewForm from "./components/ReviewForm.vue";

</script>

<template>
  <ReviewForm/>
  </template>

<style scoped>

.red {
  color: red;
}

.fz-24 {
  font-size: 24px;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
