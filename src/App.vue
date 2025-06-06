<script setup>
import { watch, ref } from 'vue';
import Number_box_with_text from './components/number_box_with_text.vue';
import Radio_group from './components/radio_group.vue'
import Speed from './components/speed.vue';

const unit_lists = {
  metric: {
    type: "metric",
    weight: "kg",
    speed: "kph",
    weight_multiplier: 1,
    speed_multiplier: 1,
  },
  imperial: {
    type: "imperial",
    weight: "lbs",
    speed: "mph",
    weight_multiplier: 2.205,
    speed_multiplier: .621371,
  },
} 
let system_in_use = ref(unit_lists["metric"].type);

let weight = ref(50);
let power = ref(200);
let drag = 0.6
let frontal_area = 0.5
let headwind = 0

</script>

<template>
  <div class="units">
    <Radio_group 
      v-model="system_in_use" 
      :unit_system="unit_lists"
      name="unit_selector"
    />
  </div>
  <div class="energy">
    <Number_box_with_text 
      text="Average Power" 
      unit="Watts" 
      :params="{min: 0, max: 2700}"
      :amount="power"
      @update:amount="$event => (power = $event)"
    />
  </div>
  <div class="weight">
    <Number_box_with_text 
      text="Rider + Bike Weight" 
      :unit="unit_lists[system_in_use].weight"  
      :params="{min: 0, max: 1000}" 
      :amount="weight"
      @update:amount="$event => (weight = $event / unit_lists[system_in_use].weight_multiplier)"
      :multiplier="unit_lists[system_in_use].weight_multiplier"
    />
  </div>
  <div class="speed">
    <Speed 
      :unit="unit_lists[system_in_use].speed"
      :power="power"
      :mass="weight"
      :drag="drag"
      :frontal_area="frontal_area"
      :headwind="headwind"
      :multiplier="unit_lists[system_in_use].speed_multiplier"
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
