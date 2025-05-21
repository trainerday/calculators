<script setup>
import { ref } from 'vue';
import Number_box_with_text from './components/number_box_with_text.vue';
import Custom_radio_form_group from './components/custom_radio_form_group.vue'

let is_metric = ref(true);
let unit_systems = ref([{
  label: "metric", 
  value: "kg"
}, {
  label: "imperial",
  value: "lbs"
}]) ;

let weight = ref(0);
let power = ref(0);
let unit = ref('kg');

</script>

<template>
  <div class="units">
    <Custom_radio_form_group 
      v-model="unit" 
      v-bind:fields="unit_systems" 
      name="unitsys" 
    />
  </div>
  <div class="energy">
    <Number_box_with_text 
      text="Average Power" 
      unit="Watts" 
      :params="{min: -100, max: 2700}"
      v-model="power"
    />
  </div>
  <div class="weight">
    <Number_box_with_text 
      text="Rider + Bike Weight" 
      :unit="unit"  
      :params="{min: 0, max: 1000}" 
      v-model="weight"
    />
  </div>
  
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
