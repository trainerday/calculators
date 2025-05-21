<script setup>
import { ref, defineProps } from 'vue';

const props = defineProps({
    fields: {
        type: Array,
        required: true,
    }
})

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
    <label v-for="(i, index) in fields" :key="index" class="radio-container"> {{ i }}
        <input type="checkbox">
        <span class = "checkmark"></span>
    </label>
    
</template>

<style scoped>

</style>
