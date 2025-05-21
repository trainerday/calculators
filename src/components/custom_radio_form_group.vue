<script setup>
import { ref, defineProps, defineModel } from 'vue';

const props = defineProps({
    fields: {
        type: Array,
        required: true,
    },
    name : {
        type: String,
        required: true,
    }
})

let selected_value = defineModel();

let should_be_checked = ref(true) ;
function check_check() {
    if (should_be_checked) {
        should_be_checked = false;
        return true;
    }
    else {
        return false;
    }
}
</script>

<template>
    <label v-for="(i, index) in fields" :key="index" class="radio-container"> {{ i.label }}
        <input type="radio" :name="name" :value="i.value" v-model="selected_value">
        <span class="checkmark"></span>
    </label>
    
</template>

<style scoped>

</style>
