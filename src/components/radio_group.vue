<script setup>
import { onMounted, ref } from 'vue' ;
const props = defineProps({
    unit_system: {
        type: Object,
        required: true,
    },
    name : {
        type: String,
        required: true,
    }
});

const selected_value = defineModel() ;

</script>

<template>
    <label v-for="i in props.unit_system" :key="i.type" class="radio-container">
        <input type="radio" :name="props.name" :value="i.type" v-model="selected_value">
        {{ i.type }}
        <!-- <span class="checkmark"></span> -->
    </label>
</template>

<style scoped>

</style>
