<script setup>
import { defineProps, reactive, provide } from 'vue';

const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  validate: {
    type: Function,
    required: true,
  },
  onSubmit: {
    type: Function,
    required: true,
  },

});

const formData = reactive({});
    const submit = (data) => {
        console.log(data)
    }
    const input = (key, value) => {
        formData[key] = value
        console.log(key, value)
    }

    provide('form:submit', submit)
    provide('form:input', input)
</script>

<template>
    <slot :submit="submit" :input="input"></slot>
</template>

<style>
</style>