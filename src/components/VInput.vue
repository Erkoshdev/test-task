<template>
  <div class="form-container" :style="{width: width}">
    <input
        :type="type"
        :value="modelValue"
        :placeholder="placeholder"
        @input="updateInput"
    >
    <slot></slot>
  </div>
</template>

<script setup>
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
@import "src/assets/scss/variables";

.form-container {
  display: flex;
  padding: var(--Indent-ind-12, 12px) var(--Indent-ind-16, 16px);
  align-items: center;
  gap: var(--Indent-ind-4, 4px);
  border-radius: var(--Radius-Rad-8, 8px);
  background: $Neutral-Neutral-100;
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