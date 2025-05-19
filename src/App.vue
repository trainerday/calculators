<script setup>
import { ref } from 'vue';

let height = ref(0);
let weight = ref(0);

function adjust(amount) {

}

function changeWeight(e) {
  weight.value = e.target.value;
  console.log(weight.value);
}
 
function changeHeight(e, scale) {

  console.log(e.target.value)
}

function al(str) {
  alert(str);
}

</script>

<template>
  <form>
    <p>Weight <input required type="number" :value="weight" @change="changeWeight($event)" id="weight" min="0" max="1000"></p>
    <p>
      Height (ft) <input required type="number" @change="changeHeight($event, 12)" id="feet" min="0" max="1000"> <br>
      (in) <input required type="number" @change="changeHeight($event, 1)" id="in" min="0" max="11"> 
    </p>

    <button type="submit" @click="adjust()">++</button>

  </form>

  <textarea v-on:keyup.s="al('Wowza');"></textarea>
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
