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
    const errors = reactive({});
    const values = ref({...props.initialValues});
    const isSubmitting = ref(false);

    const setSubmitting = (value) => {
        isSubmitting.value = value;
    }
    const resetValues = () => {
        values.value = props.initialValues;
        console.log(props.initialValues)
    }

    const handleSubmit = () => {
        setSubmitting(true);
        let tmpError = props.validate(values.value);
        Object.assign(errors, tmpError);

        if(Object.keys(tmpError).length === 0) {
            console.log('we back')
            props.onSubmit(values.value, { setSubmitting, resetValues });
        }else{
            setSubmitting(false);
        }
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
        :isSubmitting="isSubmitting"
        :values="values"></slot>
</template>

<style>
</style>