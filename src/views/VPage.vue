<template>
  <div class="table">
    <div class="table-tools">
      <div class="table-tools-left">
        <v-input v-model="search" width="360px" placeholder="Поиск">
          <VIcon icon="loup" size="size-16" color="Neutral-Neutral-500"/>
        </v-input>
      </div>
      <div class="table-tools-right">
        <v-select :options="years" v-model="selectedYears">
          <template #toggle>
            <VIcon icon="calendar" size="size-16" color="Neutral-Neutral-500"/>
            <span>Год</span>
          </template>
        </v-select>
        <v-select :options="formats" v-model="selectedFormats">
          <template #toggle>
            <VIcon icon="building" size="size-16" color="Neutral-Neutral-500"/>
            <span>Формат книги</span>
          </template>
        </v-select>
        <v-button @click="handleSearch">
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
import {ref} from "vue";
import VInput from "@/components/VInput.vue";
import VSelect from "@/components/VSelect.vue";
import VButton from "@/components/VButton.vue";
import VIcon from "@/components/VIcon.vue";
import { useCommonStore } from "@/store";

const list = ref([])
let copyList = []

const search = ref('');
const lastSearch = ref('')

function handleSearch() {
  if(search.value === lastSearch.value) {
    handleSort()
  } else {
    fetchData()
  }
}

const commonStore = useCommonStore()

function fetchData() {
  commonStore.setLoading(true);
  fetch(`https://openlibrary.org/search.json?q=${search.value}`)
      .then(res => {
        return res.json()
      })
      .then(data => {
        list.value = data.docs;
        copyList = data.docs;
        setYears(data);
        setFormats(data);
        lastSearch.value = search.value
      })
      .finally(() => {
        commonStore.setLoading(false)
      })
}

function handleSort() {
  const years = JSON.parse(JSON.stringify(selectedYears.value));
  const formats = JSON.parse(JSON.stringify(selectedFormats.value));

  if(years.length || formats.length) {
    list.value = copyList

    list.value = list.value.filter(item => {
      return years.includes(item.first_publish_year) || item.format?.some(item => formats.includes(item))
    });
  } else {
    list.value = copyList
  }
}

function compareArrays(array1, array2) {
  return array1.every(function(element, index) {
    return element === array2[index];
  });
}

const years = ref([]);
const formats = ref([]);

async function setYears(data) {
  if(!data.docs.length) return
  years.value = await data.docs.map(item => {
    return item.first_publish_year
  })
  years.value = getUnique(years.value).map(item => {
    const obj = {}
    obj.id = item;
    obj.label = item;
    return obj;
  })
}

function setFormats(data) {
  if(!data.docs.length) return
  formats.value = data.docs.map(item => {
    return item.format
  });

  formats.value = formats.value.flat();

  formats.value = getUnique(formats.value).map(item => {
    const obj = {}
    obj.id = item;
    obj.label = item;
    return obj;
  });
}

const selectedYears = ref([])
const selectedFormats = ref([])

function getUnique(arr) {
  if(!arr.length) return

  let result = [];

  for (let str of arr) {
    if (!result.includes(str)) {
      result.push(str);
    }
  }

  return result;
}

function toStringAuthors(names) {
  if(names) {
    return names.join(', ')
  } return '-'
}

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