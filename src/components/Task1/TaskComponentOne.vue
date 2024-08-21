<!-- 
Події користувача та Модіфікатори подій

Зберігання подій:
1. Створіть компонент, де кожен клік на кнопку зберігає поточний час кліка в масив і виводить цей масив на екран.
   Комбінація подій і методів:

2. Реалізуйте форму, де при submit ви використовуєте модіфікатор .prevent, і дані форми обробляються методом Vue інстанса, який також валідує їх на правильність введення перед відправкою.
   Динамічна зміна обробників подій:

3. Створіть два методи і динамічно змінюйте обробник події кліка між цими методами на основі деякої умови (наприклад, значення змінної). 
-->
<template>
  <div>
    <div className="Task 1.1">
      <button v-on:[modifier]="greet" className="btn">time</button>
      <div v-for="(item, index) in arr" :key="index">
        <h1>{{ item }}</h1>
      </div>
    </div>
    <div className="Task 1.2">
      <form @submit.prevent="onSubmit">
        <input @input="(event) => (str = event.target.value)" type="text" />
        <button className="btn">button</button>
        <h1>{{ str }}</h1>
      </form>
    </div>
    <div className="Task 1.3">
      <button v-on:[modifier]="str = 'nice'">Button</button>
      <button @click="chengeModifier">Chenge modifier</button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue"

const arr = reactive([])
const str = ref("")
const modifier = ref("click")

function chengeModifier() {
  if (modifier.value === "click") {
    modifier.value = "mouseover"
  } else {
    modifier.value = "click"
  }
}

function onSubmit(event) {
  if (event.target[0].value) {
    str.value = "good"
  }
}

function greet() {
  const today = new Date()
  const date =
    today.getFullYear() + "-" + (today.getMonth() + 1) + "-" + today.getDate()
  const time = today.getHours() + ":" + today.getMinutes()

  arr.push(date + " " + time)
}
</script>
<style scoped>
.btn {
  height: 30px;
  width: 70px;
  padding: 3px;
  background-color: rgb(106, 172, 30);
  border: none;
  font-size: 18px;
  color: white;
  cursor: pointer;
}
</style>
