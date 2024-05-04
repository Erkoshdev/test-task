<template>
  <div class="v-checkbox-group">
    <div
        class="checkbox-container"
        v-for="(option, index) in options"
        :key="index"
    >
      <input
          type="checkbox"
          :value="option.id"
          :checked="selectedOption.includes(option.id)"
          @click.capture.stop="$emit('input', $event)"
          v-model="selectedOption"
      >
      <span class="checkmark" />
      <p>{{ option.label }}</p>
    </div>
  </div>
</template>

<script setup>
import {ref, watch} from "vue";

const props = defineProps({
  options: {
    type: Array,
    default: () => []
  },
  modelValue: {
    type: Array,
    default: () => []
  },
});

const emit = defineEmits(['update', 'input'])

const selectedOption = ref(props.modelValue);

watch(selectedOption, () => {
  emit('update:modelValue', selectedOption)
});
watch(props.modelValue, (newValue) => {
  selectedOption.value = newValue;
})

// import { defineComponent } from 'vue'

// export default defineComponent({
  // name: 'VCheckboxGroup',

  // props: {
  //   options: {
  //     type: Array,
  //     default: () => []
  //   },
  //   modelValue: {
  //     type: Array,
  //     default: () => []
  //   },
  // },

  // data() {
  //   return {
  //     selectedOption: this.modelValue,
  //   }
  // },

  // watch: {
    // selectedOption() {
    //   this.$emit('update:modelValue', this.selectedOption);
    // },
    // modelValue(newValue) {
    //   this.selectedOption = newValue;
    // },
  // },
// })
</script>

<style lang="scss" scoped>
@import "src/assets/scss/variables.scss";

.checkbox-container {
  display: flex;
  padding: var(--Indent-ind-16, 16px) var(--Indent-ind-12, 12px);
  align-items: flex-start;
  gap: 12px;
  position: relative;
}
input {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  cursor: pointer;
  opacity: 0;
}
.checkmark {
  position: relative;
  width: 16px;
  height: 16px;
  border: 1px solid $Neutral-Neutral-500;
  border-radius: 5px;
  pointer-events: none;
}
.checkmark:before {
  content: '';
  background: url("@/assets/icons/checkmark.svg") no-repeat center/contain;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 10px;
  height: 7px;
  opacity: 0;
}
input:checked ~ .checkmark {
  border-color: $Primary-Blue-500;
  background: $Primary-Blue-500;
  &:before {
    opacity: 1;
  }
}
p {
  color: $Neutral-Neutral-900;
  font-size: var(--Size-Size-14, 14px);
  font-style: normal;
  font-weight: 500;
  line-height: 16px; /* 114.286% */
}
</style>