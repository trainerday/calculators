<script setup>


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
    })

    let amount = defineModel();
</script>

<template>
    <p>
        {{ text }} ({{ unit }}) <br>
        <input 
            type="number" 
            :value="amount"
            :min="(typeof params !== 'undefined') ? params.min : 0" 
            :max="(typeof params !== 'undefined') ? params.max : 1000"
        >
    </p>
</template>