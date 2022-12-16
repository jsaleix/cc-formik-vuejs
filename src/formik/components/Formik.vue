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

    const values = ref(props.initialValues);
    const isSubmitting = ref(false);
    const setSubmitting = (value) => {
        isSubmitting.value = value;
    }

    const submit = (data) => {
        console.log(data);
        setSubmitting(true);
        const errors = props.validate(values.value);
        if(Object.keys(errors).length === 0) {
            props.onSubmit(values.value, { setSubmitting });
        }
        //props.onSubmit(data, { setSubmitting });
    }

    provide('form:values', values);
    provide('form:submit', submit);
    provide('form:isSubmitting', isSubmitting);
</script>

<template>
    <slot
        :submit="submit"
        @submit.prevent="submit"
        :values="values"
        :input="input"></slot>
</template>

<style>
</style>