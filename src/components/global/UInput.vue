<script setup>

import { defineProps, defineEmits, watch, ref } from 'vue'

const { modelValue } = defineProps({
  modelValue: String,
  placeholder: String,
  type: {
    type: String,
    default: 'text',
    validator: (val) => [
        'text',
      'password',
      'tel',
      'email',
      'search',
      'textarea'].includes(val)
  }
})

const value = ref(modelValue);

watch(value, () => {
  emit('update:modelValue', newValue)
})

</script>

<template>
  <div>

    <input
        v-if="type !== 'textarea'"
        :type="type"
        :placeholder="placeholder"
        class="form-control mb-3"
        v-model="value"
    >

    <textarea
        v-else
        rows="3"
        class="form-control mb-3"
        placeholder="What do you like or not like?"
        v-model="value"
    ></textarea>
  </div>
</template>