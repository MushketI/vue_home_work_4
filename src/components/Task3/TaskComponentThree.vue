<!-- 
Директива v-for

Динамічне створення таблиці:
1. За допомогою v-for, створіть таблицю, де кількість рядків і стовпців задається динамічно через інпут або інший елемент керування.

Виведення вкладених об’єктів:
2. Реалізуйте компонент, що виводить список об'єктів, де кожен об'єкт має вкладений список. Використовуйте вкладені v-for для виведення елементів вкладеного списку.

Пагінація списку:
3. Виведіть довгий список елементів з пагінацією, використовуючи v-for, і динамічно змінюйте відображені елементи при кліку на кнопки пагінації.

4. Виведіть список елементів, використовуючи v-for, і додайте умову v-if для фільтрації елементів. 
-->

<template>
  <div>
    <div className="Task 1">
      <form @submit.prevent>
        <label for="">Columns:</label>
        <input @input="(event) => (columns = event.target.value)" type="text" />
        <label for="">lines:</label>
        <input @input="(event) => (lines = event.target.value)" type="text" />
        <button @click="createTable">Create</button>
      </form>

      <table v-for="(item, index) in tables" :key="index">
        <tr>
          <th v-for="(item, index) in new Array(item.columns)" :key="index">
            Company
          </th>
        </tr>
        <tr v-for="(item, index) in new Array(item.lines)" :key="index">
          <td>Alfreds Futterkiste</td>
        </tr>
      </table>
    </div>
    <div className="Task 2">
      <div v-for="(item, index) in arr">
        <listsComponen :lists="item.lists" :count="item.secondList.count" />
      </div>
    </div>
    <div className="Task 3">
      <div>
        <ul>
          <li v-for="p in paginatedData">
            {{ p }}
          </li>
        </ul>
        <button :disabled="pageNumber === 0" @click="prevPage">Previous</button>
        <button :disabled="pageNumber >= pageCount - 1" @click="nextPage">
          Next
        </button>
      </div>
    </div>
    <div className="Task 4">
      <div>
        <ul>
          <li v-for="number in listData">
            <span v-if="number % 2 === 0">
              {{ number }}
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive, watch, computed } from "vue"
import listsComponen from "./dop/listsComponen.vue"

const lines = ref(0)
const columns = ref(0)
const pageNumber = ref(0)
const numbers = Array.from({ length: 100 }, (v, i) => i + 1)
const size = ref(10)
const listData = reactive(numbers)

function nextPage() {
  pageNumber.value++
}

function prevPage() {
  pageNumber.value--
}

const pageCount = computed(() => {
  let l = listData.length
  let s = size.value

  return Math.ceil(l / s)
})

const paginatedData = computed(() => {
  const start = pageNumber.value * size.value
  const end = start + size.value

  return listData.slice(start, end)
})

const tables = reactive([
  {
    lines: 5,
    columns: 3,
  },
  {
    lines: 3,
    columns: 4,
  },
])

const arr = reactive([
  {
    lists: 3,
    secondList: {
      count: 5,
    },
  },
])

function createTable() {
  tables.push({
    lines: Number(lines.value),
    columns: Number(columns.value),
  })
}

watch(() => {
  pageCount
})
</script>
<style></style>
