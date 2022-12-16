<script setup>
import { defineProps} from "vue";

const props = defineProps({
    name: {
        type: String,
        required: true,
    },
    as: {
        type: String || Object,
        default: "input",
        required: true,
    },
})
</script>   

<template>
    <component :is="as" :name="name">
        <slot/>
    </component>
</template>

<style>

</style>