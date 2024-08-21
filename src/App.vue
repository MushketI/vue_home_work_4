<template>
  <div :style="{ 'background-color': theme.background, color: theme.color }">
    <TaskComponentOne />
    <TaskComponentTwo v-model="chengeTheme" />
    {{ chengeTheme }}
    {{ theme.background }}
  </div>
  <TaskComponentThree />
</template>

<script setup>
import { ref, reactive, watch } from "vue"
import TaskComponentOne from "./components/Task1/TaskComponentOne.vue"
import TaskComponentTwo from "./components/Task2/TaskComponentTwo.vue"
import TaskComponentThree from "./components/Task3/TaskComponentThree.vue"

const chengeTheme = ref(true)

const theme = reactive({
  background: "white",
  color: "black",
})

watch(() => {
  theme.background = chengeTheme.value ? "white" : "black"
  theme.color = chengeTheme.value ? "black" : "white"
})
</script>

<style scoped></style>
