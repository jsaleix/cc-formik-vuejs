<script setup>
  import { defineProps, inject } from "vue";
  const props = defineProps({
    name: {
      type: String,
      required: true,
    },
    options: {
      type: Array,
      required: true,
    },
  });

  const formData = inject("form:values");
  const errors = inject("form:errors");
</script>

<template>
  <div class="grid">
    <div
      v-bind:class="{'grid-item': true, selected: formData['captcha'] === parseInt(option.id) }"
      v-for="option in options"
    >
      <img
        :src="option.img"
        @click.exact="$emit('update:formikValue', option.id)"
      />
    </div>
    <div v-if="errors['captcha']">
      Invalid captcha
    </div>
  </div>
</template>

<style scoped>
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-items: space-around;
}
.grid-item {
  width: 30%;
}

.selected {
  border: 10px dashed rgb(43, 213, 173);
}
</style>
