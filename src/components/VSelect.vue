<template>
  <div class="select">
    <v-dropdown>
      <template #base>
        <button class="select-toggle">
          <slot name="toggle"></slot>
        </button>
      </template>
      <template #dropdown>
        <div class="select-dropdown">
          <v-input placeholder="Поиск" v-model="search" width="100%">
            <VIcon icon="loup" size="size-16" color="Neutral-Neutral-500"/>
          </v-input>
          <div class="select-dropdown-tools">
            <span>Выбрано {{ values.length }} из {{ options.length }}</span>
            <button class="clear-btn" @click="clear">Сбросить</button>
          </div>
          <div class="select-dropdown-menu">
            <v-checkbox-group :options="options" v-model="values"/>
          </div>
        </div>
      </template>
    </v-dropdown>
  </div>
</template>

<script setup>
import VDropdown from "@/components/VDropdown.vue";
import VInput from "@/components/VInput.vue";
import {ref, watch} from 'vue';
import VCheckboxGroup from "@/components/VCheckboxGroup.vue";
import VIcon from "@/components/VIcon.vue";

const props = defineProps({
  toggleName: String,
  toggleIcon: String,
  options: Array,
  disabled: Boolean
})

const emit = defineEmits(['update'])

const search = ref('');
const values = ref([]);

function clear() {
  values.value = []
}

watch(values, () => {
  emit('update:modelValue', values.value)
})

watch(search, () => {
  handleFilter()
})

function handleFilter() {
  let value = search.value.toUpperCase();
  let container = document.querySelector(".v-checkbox-group");
  let item = container.getElementsByClassName("checkbox-container");


  for (let i = 0; i < item.length; i++) {
    let txtValue = item[i].querySelector('p').innerHTML;
    if (txtValue.toUpperCase().indexOf(value) > -1) {
      item[i].style.display = "";
    } else {
      item[i].style.display = "none";
    }
  }
}

</script>

<style scoped lang="scss">
@import "src/assets/scss/variables";

.select-toggle {
  display: flex;
  padding: var(--Indent-ind-12, 12px) var(--Indent-ind-20, 20px);
  align-items: flex-start;
  gap: var(--Indent-ind-12, 12px);
  border-radius: var(--Radius-Rad-8, 8px);
  background: $Neutral-Neutral-100;
  border: none;
  cursor: pointer;
  span {
    display: block;
    color: $Neutral-Neutral-900;
    font-size: var(--Size-Size-14, 14px);
    font-style: normal;
    font-weight: 500;
    line-height: var(--Size-Size-16, 16px); /* 114.286% */
  }
}
.select-dropdown {
  border-radius: var(--Radius-Rad-8, 8px);
  border: $Neutral-Neutral-200;
  background: $Standart-White;
  box-shadow: 0 4px 64px 48px rgba(0, 0, 0, 0.05);
  padding: 8px;
}
.select-dropdown-tools {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 12px;
  span {
    color: $Neutral-Neutral-600;
    font-size: var(--Size-Size-12, 12px);
    font-style: normal;
    font-weight: 500;
    line-height: var(--Size-Size-16, 16px); /* 133.333% */
  }
}
.clear-btn {
  border: none;
  background: none;
  color: $Primary-Blue-500;
  font-size: var(--Size-Size-12, 12px);
  font-style: normal;
  font-weight: 500;
  line-height: var(--Size-Size-16, 16px); /* 133.333% */
  cursor: pointer;
}
.select-dropdown-menu {
  margin-top: 4px;
  max-height: 300px;
  overflow-y: auto;
}
.select ::v-deep(.dropdown-area) {
  left: 0;
  top: calc(100% + 16px);
}
</style>