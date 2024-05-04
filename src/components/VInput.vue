<template>
  <div class="form-container" :style="{width: props.width}">
    <input
        :type="props.type"
        :value="props.modelValue"
        :placeholder="props.placeholder"
        @input="updateInput"
    >
    <slot></slot>
  </div>
</template>

<script setup>
import {defineProps, defineEmits} from 'vue'

const emit = defineEmits(['update'])
const props = defineProps({
  type: {
    type: String,
    default: 'text'
  },
  placeholder: {
    type: String,
    default: ''
  },
  modelValue: {
    type: [String, Number],
    default: ''
  },
  width: {
    type: String,
    default: ''
  }
})

function updateInput(event) {
  emit("update:modelValue", event.target.value);
}

</script>

<style scoped lang="scss">
.form-container {
  display: flex;
  padding: var(--Indent-ind-12, 12px) var(--Indent-ind-16, 16px);
  align-items: center;
  gap: var(--Indent-ind-4, 4px);
  border-radius: var(--Radius-Rad-8, 8px);
  background: var(--Neutral-Neutral-100, #F7F9FC);
}
input {
  background: transparent;
  border: none;
  min-width: 0;
  flex: 1;
  &:focus {
    outline: none;
  }
}
</style>