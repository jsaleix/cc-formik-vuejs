<script setup>
import { defineProps, inject } from "vue";

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
    const setter = inject('form:setter');
    const formData = inject('form:values');
</script>   

<template>
    <component v-if="(typeof as === 'string')" :is="as" :name="name" :value="formData[name]" @input="(e) => setter(name, e.target.value)">
        <slot />
    </component>
    <component v-else :is="as" :name="name" v-on:update:formikValue="(value) => setter(name, value)">
        <slot />
    </component>
</template>

<style>

</style>