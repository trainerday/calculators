<script setup>
    const props = defineProps({
        img: {
            required: true,
        },
        alt: {
            required: false,
        },
        link: {
            required: true,
        },
        link_text: {
            required: false,
            type: String,
        },
        size: {
            required: false,
            type: Object,
        },
        priority: {
            required: false,
        }
    })
</script>

<template>
    <div>
        <a :href="props.link" target="_blank">{{ (props.link_text != 'undefined') ? props.link_text : '' }}
        <img 
            :src="props.img" 
            :alt="(props.alt != 'undefined') ? props.alt : ''" 
            :width="(props.size != 'undefined') ? props.size.width: null" 
            :height="(props.size != 'undefined') ? props.size.height: null"
        >
        </a>
    </div>
</template>