<script setup>
    const props = defineProps({
        group: {
            type: String,
            required: true,
        },
        text: {
            type: String,
            required: true,
        },
        data: {
            type: Array,
            required: true,
        }
    });

    const update_me = defineModel();
</script>

<template>
    {{ props.text }}
    <select v-model="update_me" :name="props.group" :id="props.group">
        <option v-for="info_group in props.data" :value="info_group.value">
            {{ info_group.name }} ({{ info_group.value }})
        </option>
    </select>
</template>

<style scoped>
    
</style>