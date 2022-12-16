<script setup>
 import { Formik, Field } from './formik';

const initialValues = {
  name: '',
  email: '',
  password: '',
};

const validate = values => {
  const errors = {};
    if (!values.email) {
      errors.email = 'Required';
    } else if (
      !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
    ) {
      errors.email = 'Invalid email address';
    }
    return errors;
  }

  const onSubmit= (values, { setSubmitting }) => {
    setTimeout(() => {
      alert(JSON.stringify(values, null, 2));
      setSubmitting(false);
    }, 400);
  }
</script>

<template>
  <main>
    <Formik
      v-slot="{ values, isSubmitting, submit }"
      :initialValues="initialValues" 
      :validate="validate" 
      :onSubmit="onSubmit">
      <form @submit.prevent="submit">
        <Field name="name" as="input"/>
        <Field name="email" as="input"/>
        <Field name="options" as="select">
          <option value="1">test1</option>
          <option value="2">test2</option>
          <option value="3">test3</option>
        </Field>
        <Field name="captcha" as="Captcha" />
        <button type="submit">Submit</button>
      </form>
    </Formik>
  </main>
</template>

<style scoped>

</style>
