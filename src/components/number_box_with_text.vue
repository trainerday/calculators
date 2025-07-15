<script setup>
import { ref, watch, computed } from 'vue';

    const props = defineProps({
        text: {
            type: String,
            required: true,
        },
        unit: {
            type: String,
            required: true,
        },
        params: {
            type: Object,
            required: false,
        },
        amount: {
            required: true,
        },
        multiplier: {
            required: false,
        },
    })

    const emit = defineEmits(["update:amount"]);
    const standard_multiplier = computed(() => (typeof props.multiplier !== 'undefined') ? props.multiplier : 1 );
    // watch(
    //     standard_multiplier,
    //     (newVal) => {
    //         val.value = Math.round(newVal) ;
    //     }
    // )
</script>

<template>
    <div>
        {{ text }} ({{ unit }})
        <input 
            type="number" 
            :value="props.amount * standard_multiplier"
            @input="emit('update:amount', $event.target.value)"
            :min="(typeof params !== 'undefined') ? params.min : 0" 
            :max="(typeof params !== 'undefined') ? params.max : 1000"
        >
    </div>
</template>

<style scoped>
    div {
        display: flex;
        flex-direction: column;
        text-align: center;
        align-items: center;
        justify-content: center;
    }
</style>