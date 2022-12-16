<script setup>
 import { Formik, Field } from './formik';

</script>

<template>
  <main>
    <Formik>
      <form>
        <Field name="name" as="input"/>
        <Field name="email" as="input"/>
        <Field name="options" as="select">
          <option value="1">test1</option>
          <option value="2">test2</option>
          <option value="3">test3</option>
        </Field>
        <Field name="captcha" as="Captcha" />

      </form>
    </Formik>
  </main>
</template>

<style scoped>

</style>
