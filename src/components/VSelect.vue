<template>
  <div class="select">
    <v-dropdown>
      <template #base>
        <button class="select-toggle">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M4.66732 1.99984V0.666504H6.00065V1.99984H10.0007V0.666504H11.334V1.99984H14.0007C14.3689 1.99984 14.6673 2.29832 14.6673 2.6665V5.99984H13.334V3.33317H11.334V4.6665H10.0007V3.33317H6.00065V4.6665H4.66732V3.33317H2.66732V12.6665H6.66732V13.9998H2.00065C1.63246 13.9998 1.33398 13.7014 1.33398 13.3332V2.6665C1.33398 2.29832 1.63246 1.99984 2.00065 1.99984H4.66732ZM11.334 7.99984C9.86125 7.99984 8.66732 9.19377 8.66732 10.6665C8.66732 12.1392 9.86125 13.3332 11.334 13.3332C12.8067 13.3332 14.0007 12.1392 14.0007 10.6665C14.0007 9.19377 12.8067 7.99984 11.334 7.99984ZM7.33398 10.6665C7.33398 8.45737 9.12485 6.6665 11.334 6.6665C13.5431 6.6665 15.334 8.45737 15.334 10.6665C15.334 12.8756 13.5431 14.6665 11.334 14.6665C9.12485 14.6665 7.33398 12.8756 7.33398 10.6665ZM10.6673 8.6665V10.9426L12.1959 12.4712L13.1387 11.5284L12.0007 10.3904V8.6665H10.6673Z" fill="#98A2B3"/>
          </svg>
          <span>Год</span>
        </button>
      </template>
      <template #dropdown>
        <div class="select-dropdown">
          <v-input placeholder="Поиск" v-model="search" width="100%">
            <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M11.0156 10.0781L13.875 12.9375L12.9375 13.875L10.0781 11.0156C9.56771 11.4323 8.98958 11.7552 8.34375 11.9844C7.70833 12.2135 7.03646 12.3281 6.32812 12.3281C5.50521 12.3281 4.72917 12.1719 4 11.8594C3.27083 11.5469 2.63542 11.1198 2.09375 10.5781C1.55208 10.0365 1.125 9.40104 0.8125 8.67188C0.489583 7.94271 0.328125 7.16146 0.328125 6.32812C0.328125 5.50521 0.489583 4.72917 0.8125 4C1.125 3.27083 1.55208 2.63542 2.09375 2.09375C2.63542 1.55208 3.27083 1.125 4 0.8125C4.72917 0.489583 5.50521 0.328125 6.32812 0.328125C7.16146 0.328125 7.94271 0.489583 8.67188 0.8125C9.40104 1.125 10.0365 1.55208 10.5781 2.09375C11.1198 2.63542 11.5469 3.27083 11.8594 4C12.1719 4.72917 12.3281 5.50521 12.3281 6.32812C12.3281 7.03646 12.2135 7.71354 11.9844 8.35938C11.7552 8.99479 11.4323 9.56771 11.0156 10.0781ZM9.6875 9.57812C10.0938 9.16146 10.4115 8.67708 10.6406 8.125C10.8802 7.5625 11 6.96354 11 6.32812C11 5.68229 10.8802 5.07812 10.6406 4.51562C10.3906 3.95312 10.0521 3.46354 9.625 3.04688C9.20833 2.61979 8.71875 2.28125 8.15625 2.03125C7.58333 1.79167 6.97396 1.67188 6.32812 1.67188C5.68229 1.67188 5.07812 1.79167 4.51562 2.03125C3.95312 2.28125 3.45833 2.61979 3.03125 3.04688C2.61458 3.46354 2.28125 3.95312 2.03125 4.51562C1.79167 5.07812 1.67188 5.68229 1.67188 6.32812C1.67188 6.97396 1.79167 7.58333 2.03125 8.15625C2.28125 8.71875 2.61458 9.21354 3.03125 9.64062C3.45833 10.0573 3.95312 10.3906 4.51562 10.6406C5.07812 10.8802 5.68229 11 6.32812 11C6.96354 11 7.55729 10.8854 8.10938 10.6562C8.67188 10.4167 9.16146 10.0938 9.57812 9.6875L9.6875 9.57812Z" fill="#98A2B3"/>
            </svg>
          </v-input>
          <div class="select-dropdown-tools">
            <span>Выбрано 3 из 17</span>
            <button class="clear-btn" @click="clear">Сбросить</button>
          </div>
          <div class="select-dropdown-menu">
            <v-checkbox-group :options="arr" v-model="values"/>
          </div>
        </div>
      </template>
    </v-dropdown>
  </div>
</template>

<script setup>
import VDropdown from "@/components/VDropdown.vue";
import VInput from "@/components/VInput.vue";
import {ref} from 'vue';
import VCheckboxGroup from "@/components/VCheckboxGroup.vue";

const arr = [{label: 1951, id: 1}, {label: 1951, id: 1}, {label: 1951, id: 1}, {label: 1951, id: 1}]

const search = ref('');
const values = ref([]);

function clear() {
  console.log('clear')
}
</script>

<style scoped lang="scss">
.select-toggle {
  display: flex;
  padding: var(--Indent-ind-12, 12px) var(--Indent-ind-20, 20px);
  align-items: flex-start;
  gap: var(--Indent-ind-12, 12px);
  border-radius: var(--Radius-Rad-8, 8px);
  background: var(--Neutral-Neutral-100, #F7F9FC);
  border: none;
  cursor: pointer;
  span {
    display: block;
    color: var(--Neutral-Neutral-900, #1D2739);
    font-size: var(--Size-Size-14, 14px);
    font-style: normal;
    font-weight: 500;
    line-height: var(--Size-Size-16, 16px); /* 114.286% */
  }
}
.select-dropdown {
  border-radius: var(--Radius-Rad-8, 8px);
  border: 1px solid var(--Neutral-Neutral-200, #F0F2F5);
  background: var(--Standart-White, #FFF);
  box-shadow: 0px 4px 64px 48px rgba(0, 0, 0, 0.05);
  padding: 8px;
}
.select-dropdown-tools {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 12px;
  span {
    color: var(--Neutral-Neutral-600, #667185);
    font-size: var(--Size-Size-12, 12px);
    font-style: normal;
    font-weight: 500;
    line-height: var(--Size-Size-16, 16px); /* 133.333% */
  }
}
.clear-btn {
  border: none;
  background: none;
  color: var(--Primary-Blue-500, #007BFF);
  font-size: var(--Size-Size-12, 12px);
  font-style: normal;
  font-weight: 500;
  line-height: var(--Size-Size-16, 16px); /* 133.333% */
  cursor: pointer;
}
.select-dropdown-menu {
  margin-top: 4px;
}
.select ::v-deep(.dropdown-area) {
  left: 0;
  top: calc(100% + 16px);
}
</style>