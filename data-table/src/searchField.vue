<script setup lang="ts">
const searchTerm = defineModel<string>();
</script>

<template>
  <input
    class="bg-zinc-200 text-zinc-600 font-mono ring-1 ring-zinc-400 focus:ring-2 focus:ring-blue-200 outline-none duration-300 placeholder:text-zinc-600 placeholder:opacity-50 rounded-full px-4 py-2 shadow-md focus:shadow-lg focus:shadow-blue-200 dark:shadow-md dark:shadow-mauve-200"
    autocomplete="off"
    placeholder="Search here..."
    name="search"
    type="text"
    v-model="searchTerm"
  />
</template>

