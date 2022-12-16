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
    <component v-if="(typeof as === 'string')" :is="as" :name="name"/>
    <component v-else :is="as" :name="name" />
</template>

<style>

</style>