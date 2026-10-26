<script setup lang="ts">

import Loading from './loading.vue';
import SearchableTable from './searchableTable.vue';

</script>

<template>
		<Suspense>
  		<div class="flex flex-row justify-around items-center h-screen max-w-full relative">
			<SearchableTable :dataUrl="'http://localhost:8080/csvtojson?filename=src/main/java/com/example/testCsvFiles/test.csv'" />
			<SearchableTable :dataUrl="'http://localhost:8080/csvtojson?filename=src/main/java/com/example/testCsvFiles/test.csv'" />
  		</div>
		<template #fallback>
			<Loading />
		</template>
  	</Suspense>
</template>

<style scoped></style>
