<template>
  <div class="table">
    <div class="table-tools">
      <div class="table-tools-left">
        <v-input v-model="search" width="360px" placeholder="Поиск">
          <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M11.0156 10.0781L13.875 12.9375L12.9375 13.875L10.0781 11.0156C9.56771 11.4323 8.98958 11.7552 8.34375 11.9844C7.70833 12.2135 7.03646 12.3281 6.32812 12.3281C5.50521 12.3281 4.72917 12.1719 4 11.8594C3.27083 11.5469 2.63542 11.1198 2.09375 10.5781C1.55208 10.0365 1.125 9.40104 0.8125 8.67188C0.489583 7.94271 0.328125 7.16146 0.328125 6.32812C0.328125 5.50521 0.489583 4.72917 0.8125 4C1.125 3.27083 1.55208 2.63542 2.09375 2.09375C2.63542 1.55208 3.27083 1.125 4 0.8125C4.72917 0.489583 5.50521 0.328125 6.32812 0.328125C7.16146 0.328125 7.94271 0.489583 8.67188 0.8125C9.40104 1.125 10.0365 1.55208 10.5781 2.09375C11.1198 2.63542 11.5469 3.27083 11.8594 4C12.1719 4.72917 12.3281 5.50521 12.3281 6.32812C12.3281 7.03646 12.2135 7.71354 11.9844 8.35938C11.7552 8.99479 11.4323 9.56771 11.0156 10.0781ZM9.6875 9.57812C10.0938 9.16146 10.4115 8.67708 10.6406 8.125C10.8802 7.5625 11 6.96354 11 6.32812C11 5.68229 10.8802 5.07812 10.6406 4.51562C10.3906 3.95312 10.0521 3.46354 9.625 3.04688C9.20833 2.61979 8.71875 2.28125 8.15625 2.03125C7.58333 1.79167 6.97396 1.67188 6.32812 1.67188C5.68229 1.67188 5.07812 1.79167 4.51562 2.03125C3.95312 2.28125 3.45833 2.61979 3.03125 3.04688C2.61458 3.46354 2.28125 3.95312 2.03125 4.51562C1.79167 5.07812 1.67188 5.68229 1.67188 6.32812C1.67188 6.97396 1.79167 7.58333 2.03125 8.15625C2.28125 8.71875 2.61458 9.21354 3.03125 9.64062C3.45833 10.0573 3.95312 10.3906 4.51562 10.6406C5.07812 10.8802 5.68229 11 6.32812 11C6.96354 11 7.55729 10.8854 8.10938 10.6562C8.67188 10.4167 9.16146 10.0938 9.57812 9.6875L9.6875 9.57812Z" fill="#98A2B3"/>
          </svg>
        </v-input>
      </div>
      <div class="table-tools-right">
        <v-select></v-select>
        <v-button>
          <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M11.0156 10.0781L13.875 12.9375L12.9375 13.875L10.0781 11.0156C9.56771 11.4323 8.98958 11.7552 8.34375 11.9844C7.70833 12.2135 7.03646 12.3281 6.32812 12.3281C5.50521 12.3281 4.72917 12.1719 4 11.8594C3.27083 11.5469 2.63542 11.1198 2.09375 10.5781C1.55208 10.0365 1.125 9.40104 0.8125 8.67188C0.489583 7.94271 0.328125 7.16146 0.328125 6.32812C0.328125 5.50521 0.489583 4.72917 0.8125 4C1.125 3.27083 1.55208 2.63542 2.09375 2.09375C2.63542 1.55208 3.27083 1.125 4 0.8125C4.72917 0.489583 5.50521 0.328125 6.32812 0.328125C7.16146 0.328125 7.94271 0.489583 8.67188 0.8125C9.40104 1.125 10.0365 1.55208 10.5781 2.09375C11.1198 2.63542 11.5469 3.27083 11.8594 4C12.1719 4.72917 12.3281 5.50521 12.3281 6.32812C12.3281 7.03646 12.2135 7.71354 11.9844 8.35938C11.7552 8.99479 11.4323 9.56771 11.0156 10.0781ZM9.6875 9.57812C10.0938 9.16146 10.4115 8.67708 10.6406 8.125C10.8802 7.5625 11 6.96354 11 6.32812C11 5.68229 10.8802 5.07812 10.6406 4.51562C10.3906 3.95312 10.0521 3.46354 9.625 3.04688C9.20833 2.61979 8.71875 2.28125 8.15625 2.03125C7.58333 1.79167 6.97396 1.67188 6.32812 1.67188C5.68229 1.67188 5.07812 1.79167 4.51562 2.03125C3.95312 2.28125 3.45833 2.61979 3.03125 3.04688C2.61458 3.46354 2.28125 3.95312 2.03125 4.51562C1.79167 5.07812 1.67188 5.68229 1.67188 6.32812C1.67188 6.97396 1.79167 7.58333 2.03125 8.15625C2.28125 8.71875 2.61458 9.21354 3.03125 9.64062C3.45833 10.0573 3.95312 10.3906 4.51562 10.6406C5.07812 10.8802 5.68229 11 6.32812 11C6.96354 11 7.55729 10.8854 8.10938 10.6562C8.67188 10.4167 9.16146 10.0938 9.57812 9.6875L9.6875 9.57812Z" fill="white"/>
          </svg>
          Поиск
        </v-button>
      </div>
    </div>
    <div class="table-header">
      <div class="table-data">Название</div>
      <div class="table-data">Автор</div>
      <div class="table-data">Год издания</div>
      <div class="table-data">Формат книги</div>
    </div>
    <div class="table-row" v-for="item in list" :key="item.key">
      <div class="table-data">
        <p>{{ item.title }}</p>
      </div>
      <div class="table-data">
        <p>{{ toStringAuthors(item.author_name) }}</p>
      </div>
      <div class="table-data">
        <p>{{ item.first_publish_year ??= '-' }}</p>
      </div>
      <div class="table-data book-formats">
        <span class="book-format" v-for="(format, formatIdx) in item.format" :key="formatIdx">{{ format }}</span>
      </div>
    </div>
  </div>

</template>

<script setup>
import VInput from "@/components/VInput.vue";
import {onMounted, ref} from "vue";
import VSelect from "@/components/VSelect.vue";
import VButton from "@/components/VButton.vue";

onMounted(() => {
  fetchData();
})

const list = ref([])
function fetchData() {
  fetch('https://openlibrary.org/search.json?q=the+lord+of+the+rings')
      .then(res => {
        return res.json()
      })
      .then(data => {
        list.value = data.docs;
      })
}

function toStringAuthors(names) {
  if(names) {
    return names.join(', ')
  } return '-'
}

const search = ref('');

</script>

<style lang="scss" scoped>
.table {
  border-radius: 16px;
  border: 1px solid #F0F2F5;
  background: #FFF;
  margin-top: 16px;
  overflow: hidden;
}
.table-tools {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #fff;
  padding: var(--Indent-ind-12, 12px) var(--Indent-ind-24, 24px);
}
.table-tools-right {
  display: flex;
  align-items: center;
  gap: 12px;
}
.table-data {
  &:nth-of-type(1) {
    width: 17%;
  }
  &:nth-of-type(2) {
    width: 13%;
  }
  &:nth-of-type(3) {
    width: 9%;
  }
  &:nth-of-type(4) {
    width: 61%;
  }
}
.table-header {
  display: flex;
  background: #F7F9FC;
  .table-data {
    padding: 12px 24px;
    color: #667185;
    font-size: 12px;
    font-style: normal;
    font-weight: 500;
    line-height: 16px;
  }
}
.table-row {
  display: flex;
  border-bottom: 1px solid #F0F2F5;
  background: #FFF;
  &:last-child {
    border-bottom: none;
  }
  .table-data {
    padding: 24px;
    height: fit-content;
    min-height: 72px;
    display: flex;
    align-items: center;
  }
  .table-data p {
    color: #1D2739;
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 16px;
    max-width: 100%;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
}
.book-formats {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}
.book-format {
  padding: 4px 8px;
  border-radius: 8px;
  background: #E6F2FF;
  color: #1D2739;
  font-size: 12px;
  font-style: normal;
  font-weight: 400;
  line-height: 16px;
}
</style>