<script setup>
  import { Formik, Field } from './formik';
  import Captcha from './components/Captcha.vue';

  const options = [
  {
    id: 1,
    img: "https://picsum.photos/200?random=1",
  },
  {
    id: 2,
    img: "https://picsum.photos/200?random=2",
  },
  {
    id: 3,
    img: "https://picsum.photos/200?random=3",
  },
  {
    id: 4,
    img: "https://picsum.photos/200?random=4",
  },
  {
    id: 5,
    img: "https://picsum.photos/200?random=5",
  },
  {
    id: 6,
    img: "https://picsum.photos/200?random=6",
  },
];

  const initialValues = {
    name: 'test',
    email: 'test@mail.com',
    select: 1,
    captcha: -1,
  };

  const validate = values => {
      const tmpErrors = {};
      if(options.find(option => option.id === values.captcha) === undefined) {
        tmpErrors.captcha = 'Required';
      }
      if(values.name === 'test') {
        tmpErrors.name = 'Invalid name';
      }
      console.log('apres', tmpErrors)
      if(Object.entries(tmpErrors).length === 0){
        return {};
      }
      return tmpErrors;
  }

  const onSubmit= (values, { setSubmitting, resetValues }) => {
    setTimeout(() => {
      setSubmitting(false);
      alert(JSON.stringify(values, null, 2));
      resetValues();
    }, 1000);
  }


</script>

<template>
  <main>
    <Formik
      v-slot="{ values, isSubmitting, handleSubmit, errors }"
      :initialValues="initialValues" 
      :validate="validate" 
      :onSubmit="onSubmit">
      <template v-if="isSubmitting">
        Submitting...
        </template>
      <template v-else>
        <template v-if="Object.entries(errors).length > 0">
          Invalid form
        </template>
        <form @submit.prevent="handleSubmit">
          <Field name="name" as="input"/>
          <Field name="email" as="input"/>
          <Field name="select" as="select">
            <option value="1">test1</option>
            <option value="2">test2</option>
            <option value="3">test3</option>
          </Field>
          <Field name="captcha" :as="Captcha" :options="options"/>
          <button type="submit">Submit</button>
        </form>
      </template>
    </Formik>
  </main>
</template>

<style scoped>

</style>
