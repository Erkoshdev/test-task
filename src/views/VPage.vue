<template>
  <div class="table">
    <div class="table-tools">
      <div class="table-tools-left">
        <v-input v-model="search" width="360px" placeholder="Поиск">
          <VIcon icon="loup" size="size-16" color="Neutral-Neutral-500"/>
        </v-input>
      </div>
      <div class="table-tools-right">
        <v-select :options="[{label: 1951, id: 1}, {label: 1951, id: 2}, {label: 1951, id: 3}, {label: 1951, id: 4}]">
          <template #toggle>
            <VIcon icon="calendar" size="size-16" color="Neutral-Neutral-500"/>
            <span>Год</span>
          </template>
        </v-select>
        <v-select :options="[{label: 'Аудиокнига', id: 1}, {label: 'DVD диск', id: 2}, {label: 'Бумажный', id: 3}, {label: 'Твердый переплет', id: 4}, {label: 'Audio CD', id: 5}]">
          <template #toggle>
            <VIcon icon="building" size="size-16" color="Neutral-Neutral-500"/>
            <span>Формат книги</span>
          </template>
        </v-select>
        <v-button>
          <VIcon icon="loup" size="size-16" color="Standart-White"/>
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
import VIcon from "@/components/VIcon.vue";

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
@import "src/assets/scss/variables";

.table {
  border: 1px solid $Neutral-Neutral-200;
  background: #FFF;
  margin-top: 16px;
  border-radius: 16px;
}
.table-tools {
  border-radius: 16px 16px 0 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: $Standart-White;
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
  background: $Neutral-Neutral-100;
  .table-data {
    padding: 12px 24px;
    color: $Neutral-Neutral-600;
    font-size: 12px;
    font-style: normal;
    font-weight: 500;
    line-height: 16px;
  }
}
.table-row {
  display: flex;
  border-bottom: 1px solid $Neutral-Neutral-200;
  background: $Standart-White;
  &:last-child {
    border-bottom: none;
    border-radius: 0 0 16px 16px;
  }
  .table-data {
    padding: 24px;
    height: fit-content;
    min-height: 72px;
    display: flex;
    align-items: center;
  }
  .table-data p {
    color: $Neutral-Neutral-900;
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
  background: $Primary-Blue-50;
  color: $Neutral-Neutral-900;
  font-size: 12px;
  font-style: normal;
  font-weight: 400;
  line-height: 16px;
}
</style>