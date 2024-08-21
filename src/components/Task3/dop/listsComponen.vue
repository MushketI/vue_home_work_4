<template>
  <div v-for="(item, index) in new Array(lists)" :key="index">
    <select>
      <option
        v-for="(items, index) in new Array(count)"
        :key="index"
        value="free"
      >
        Free
      </option>
    </select>
  </div>
</template>
<script setup>
defineProps({
  lists: Number,
  count: Number,
})
</script>
<style scoped></style>
