<script setup>
    import { defineProps, reactive, provide, ref, watch } from 'vue';
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
    let errors = reactive({});
    const values = ref(props.initialValues);
    const isSubmitting = ref(false);
    const setSubmitting = (value) => {
        isSubmitting.value = value;
    }

    const handleSubmit = () => {
        console.log("submit called");
        setSubmitting(true);
        errors = props.validate(values.value);
        if(Object.keys(errors).length === 0) {
            props.onSubmit(values.value, { setSubmitting });
        }
        console.log(errors);
    }

    provide('form:values', values);
    provide('form:handleSubmit', handleSubmit);
    provide('form:isSubmitting', isSubmitting);
    provide('form:errors', errors);
    provide('form:setter', (name, value) => {
        values.value[name] = value;
    });
</script>

<template>
    <slot
        :handleSubmit="handleSubmit"
        @submit.prevent="handleSubmit"
        :errors="errors"
        :values="values"
        :input="input"></slot>
</template>

<style>
</style>