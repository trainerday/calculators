<script setup>
import { ref } from 'vue';
import Number_box_with_text from './number_box_with_text.vue';
import Radio_group from './radio_group.vue'
import Speed from './speed.vue';
import Select_group from './select_group.vue';

const unit_lists = {
    metric: {
        type: "metric",
        weight: "kg",
        speed: "km/h",
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
const drags = [
    {
        name: "Tops",
        value: 0.5
    },
    {
        name: "Hoods + 20% on Drops",
        value: 0.4
    },
    {
        name: "Aero",
        value: 0.3
    }
]
let drag = ref(drags[0].value);

</script>

<template>
    <div class="container">
        <div class="units">
            Units:
            <Radio_group
                v-model="system_in_use" 
                :unit_system="unit_lists" 
                name="unit_selector" 
            />
        </div>
        <div class="numbers-with-text">
            <span class="energy">
                <Number_box_with_text 
                    text="Average Power" unit="Watts" 
                    :params="{ min: 0, max: 2700 }" 
                    :amount="power"
                    @update:amount="$event => (power = $event)" 
                />
            </span>
            <span class="weight">
                <Number_box_with_text text="Rider + Bike Weight" 
                    :unit="unit_lists[system_in_use].weight"
                    :params="{ min: 0, max: 1000 }" 
                    :amount="weight"
                    @update:amount="$event => (weight = $event / unit_lists[system_in_use].weight_multiplier)"
                    :multiplier="unit_lists[system_in_use].weight_multiplier" 
                />
            </span>
        </div>
        <div>
            <span class="drag">
                <Select_group 
                    group="drag" 
                    text="Choose a drag value" 
                    :data="drags" 
                    v-model="drag" 
                />
            </span>
        </div>
        <div>
            <span class="speed">
                <Speed 
                    :unit="unit_lists[system_in_use].speed" 
                    :power="power" 
                    :mass="weight" 
                    :drag="drag" 
                    :frontal_area=".5"
                    :headwind="0" 
                    :multiplier="unit_lists[system_in_use].speed_multiplier" 
                />
                <Speed 
                    :unit="unit_lists[system_in_use].speed" 
                    :power="power" 
                    :mass="weight" 
                    :drag="drag" 
                    :frontal_area=".5"
                    :headwind="5" 
                    :multiplier="unit_lists[system_in_use].speed_multiplier" 
                />
            </span>
        </div>
    </div>
</template>

<style scoped>
    p {
        display: inherit;
    }

    .top {
        padding: 4%;
    }

    .container {
        display: flex;
        flex-direction: column;
    }

    .numbers-with-text {
        display: inherit;
        flex-direction: row;
        justify-content: space-evenly;
    }

    .units {
        display: flex;
    }

    
</style>
