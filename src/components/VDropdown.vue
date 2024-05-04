<template>
  <div class="dropdown" :class="{ active: show }" ref="container">
    <div class="dropdown-base" @click="handleShow">
      <slot name="base" :handleShow="handleShow" />
    </div>
    <div v-if="show" class="dropdown-area">
      <slot name="dropdown" :handleShow="handleShow" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const show = ref(false);
const container = ref();

const close = (event) => {
  if(container.value.contains(event.target)) return
  else {
    show.value = false;
  }
}
const handleShow = () => {
  show.value = !show.value
}
onMounted(() => {
  document.addEventListener('click', close);
});
onBeforeUnmount(() => {
  document.removeEventListener('click', this.close);
})
</script>

<style scoped lang="scss">
.dropdown {
  position: relative;
}
.dropdown-area {
  position: absolute;
}
</style>