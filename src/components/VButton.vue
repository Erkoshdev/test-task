<template>
  <button
      class="btn"
      :class="type"
      @click="$emit('click')"
  >
    <slot></slot>
  </button>
</template>

<script setup>
import {defineProps, defineEmits} from 'vue';

const emits = defineEmits(['click'])
const props = defineProps({
  type: {
    type: String,
    default: 'primary'
  }
})
</script>

<style scoped>
.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--Indent-ind-12, 12px) var(--Indent-ind-20, 20px);
  gap: var(--Indent-ind-12, 12px);
  border-radius: var(--Radius-Rad-8, 8px);
  font-size: var(--Size-Size-14, 14px);
  font-style: normal;
  font-weight: 500;
  line-height: var(--Size-Size-16, 16px); /* 114.286% */
  border: none;
  transition: 0.2s ease;
  &:active {
    transform: scale(0.9);
  }
}
.primary {
  background: var(--Primary-Blue-500, #007BFF);
  color: var(--Standart-White, #FFF);
}
</style>
