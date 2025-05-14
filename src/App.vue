<!-- <script setup>

</script> -->

<template>
  <form>
    <p>Weight <input required type="number" id="weight" min="0" max="1000"></p>
    <p>
      Height (ft) <input required type="number" id="feet" min="0" max="1000"> <br>
      (in) <input required type="number" id="feet" min="0" max="11"> 
    </p>

  </form>
</template>

<style scoped>
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
