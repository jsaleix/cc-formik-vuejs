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
    watch( () => {
        if(isSubmitting.value) {
            const errors = props.validate(values.value);
            if(Object.keys(errors).length === 0) {
                props.onSubmit(values.value, { setSubmitting });
            }
        }
    }, isSubmitting.value);

    const formData = reactive({});
    const submit = (data) => {
        console.log(data);
        props.onSubmit(data, { setSubmitting });
    }


    provide('form:submit', submit);
    provide('form:isSubmitting', isSubmitting);
</script>

<template>
    <slot :submit="submit" :input="input"></slot>
</template>

<style>
</style>