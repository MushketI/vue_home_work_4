<!-- 
Динамічні Стилі

Стилізація списку:
1. Створіть динамічний список елементів, де кожен елемент має випадковий колір фону та розмір шрифту, згенеровані методом при створенні компоненту.

Анімації елементів:
2. Реалізуйте динамічне змінення стилів елемента (наприклад, зміна позиції, коліру, розміру) за допомогою CSS Transitions або Animations при натисканні кнопки.
   Темна та Світла Теми:

3. Створіть переключатель тем, який динамічно змінює стилі всього додатку між темною та світлою темами. 
-->

<template>
  <div className="div">
    <div className="Task 1">
      <ul v-for="(item, index) in arr" :key="index">
        <li :style="{ 'font-size': item.size, 'background-color': item.color }">
          {{ item.text }}
        </li>
      </ul>
      <button @click="generateColor">click</button>
    </div>
    <div className="Task 2">
      <button @click="show = !show">Click</button>
      <transition name="slide-fade">
        <div v-if="show" className="kub"></div>
      </transition>
    </div>
    <div className="Task 3">
      <button @click="update">Theme</button>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive, watch, defineModel } from "vue"

defineProps({
  chengeTheme: Boolean,
})

const model = defineModel()

function update() {
  model.value = !model.value
}

const arr = reactive([
  { text: "One", color: "", size: "" },
  { text: "Two", color: "", size: "" },
  { text: "three", color: "", size: "" },
])

const show = ref(false)

function generateColor() {
  arr.map((item) => {
    item.color = "#" + (Math.random().toString(16) + "000000").substring(2, 8)
    item.size = Math.floor(Math.random() * 25) + 16 + "px"
  })
}

watch(() => {
  generateColor()
})
</script>
<style scoped>
li {
  height: 70px;
}

.div {
  flex-wrap: wrap;
  width: 100%;
}
.kub {
  margin-top: 20px;
  width: 100px;
  height: 100px;
  background-color: gold;
  opacity: 0.7;
}

.slide-fade-enter-active {
  transition: all 1s ease-out;
}

.slide-fade-leave-active {
  transition: all 1s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  margin-left: 250px;
  transform: translateX(100px);
}
</style>
