<script setup>
import { ref, watch } from 'vue';
import Number_box_with_text from './number_box_with_text.vue';
import Radio_group from './radio_group.vue'
import Speed from './speed.vue';
import Select_group from './select_group.vue';

import tops from '@/assets/Tops.png'
import hoods from '@/assets/Hoods.png'
import aero from '@/assets/Aero.png'

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
        img: tops,
        value: 0.5
    },
    {
        name: "Hoods + 20% on Drops",
        img: hoods,
        value: 0.4
    },
    {
        name: "Aero",
        img: aero,
        value: 0.3
    }
]
let drag = ref(drags[0].value);

let drag_image = ref(drags[0].img)
watch(drag, () => {
    for (let i in drags) {
        // console.log(drag.value, drags[i], drag.value == drags[i].value)
        if (drag.value == drags[i].value) {
            drag_image.value = drags[i].img;
            break;
        }
    }
})

</script>

<template>
    <div class="container">
        <h2>Cycling Power-to-Speed Calculator</h2>
        <p>
            Estimate your cycling speed based on power output <br>
            and conditions <a href="https://gribble.org/cycling/power_v_speed.html" target="_blank">Learn More</a>
        </p>
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
        <span class="drag">
            <Select_group 
                group="drag" 
                text="Choose a drag value:" 
                :data="drags" 
                v-model="drag" 
            />
            <div class="image">
                <img :src="drag_image">
            </div>
        </span>
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
    h2 {
        margin-top: 1.5rem;
        margin-bottom: 0;
    }

    p {
        margin-top: 0;
    }

    a {
        font-size: medium;
    }

    .top {
        padding: 4%;
    }

    .container {
        display: flex;
        flex-direction: column;
        text-align: center;
        gap: 1.25rem;
        padding: 0px 10% 1.5rem 10%;
    }

    .units {

    }

    .numbers-with-text {
        display: inherit;
        flex-direction: row;
        justify-content: space-evenly;
    }

    .drag {
        display: grid;
        justify-content: center;
        align-items: center;
        grid-template-areas: 
            '. drag-image'
            '. drag-image';
    }

    .image {
        display: flex;
        grid-area: drag-image;
        height: 90px;
        width: 250px;
        justify-content: center;
        align-items: center;
    }

    .image > img {
        object-fit: contain;
        width: 100%;
        height: 100%;
    }

    .speed {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        text-justify: center;
    }
    
    @media (max-width: 800px) {
        .drag {
            display: flex;
            flex-direction: column;
            gap: 7px;
        }
    }
</style>
