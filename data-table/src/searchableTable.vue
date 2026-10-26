<script setup lang="ts">
import { computed } from 'vue';
import BasicTable from './basicTable.vue';
import SearchField from './searchField.vue';

const searchTerm = defineModel<string>({ default: '' });

const props = defineProps({
  dataUrl: {
    type: String,
    required: true
  },
});


// const tableData = [
// 	{
// 		"id": 1,
// 		"date": "Oct 21, 2026",
// 		"time": "9:31 AM",
// 		"city": "Mulhouse",
// 		"valid data": "No",
// 		"normaldist": -0.1167989987,
// 		"list": "3, 10"
// 	},
// 	{
// 		"id": 2,
// 		"date": "Jun 9, 2027",
// 		"time": "1:32 AM",
// 		"city": "Hard",
// 		"valid data": "Yes",
// 		"normaldist": -0.2432235513,
// 		"list": "8, 3, 4, 10"
// 	},
// 	{
// 		"id": 3,
// 		"date": "May 26, 2027",
// 		"time": "3:06 AM",
// 		"city": "Santander",
// 		"valid data": "No",
// 		"normaldist": -0.0905788876,
// 		"list": "8, 6, 10, 1"
// 	},
// 	{
// 		"id": 4,
// 		"date": "Aug 4, 2027",
// 		"time": "5:36 PM",
// 		"city": "Panguipulli",
// 		"valid data": "Yes",
// 		"normaldist": "0.1818643060",
// 		"list": "8, 10, 6, 9"
// 	},
// 	{
// 		"id": 5,
// 		"date": "Apr 29, 2026",
// 		"time": "3:50 PM",
// 		"city": "Xalapa",
// 		"valid data": "No",
// 		"normaldist": "0.0440661079",
// 		"list": "4, 6"
// 	},
// 	{
// 		"id": 6,
// 		"date": "Dec 13, 2026",
// 		"time": "2:08 AM",
// 		"city": "Rishra",
// 		"valid data": "Yes",
// 		"normaldist": -0.0724024632,
// 		"list": "5, 4, 8, 6, 1"
// 	},
// 	{
// 		"id": 7,
// 		"date": "Jun 15, 2026",
// 		"time": "5:34 PM",
// 		"city": "Okene",
// 		"valid data": "Yes",
// 		"normaldist": -0.0845340764,
// 		"list": "9, 2, 4, 10, 8"
// 	},
// 	{
// 		"id": 8,
// 		"date": "Jan 6, 2027",
// 		"time": "10:34 PM",
// 		"city": "Workum",
// 		"valid data": "Yes",
// 		"normaldist": -0.3824679759,
// 		"list": "4, 7, 6"
// 	},
// 	{
// 		"id": 9,
// 		"date": "May 25, 2027",
// 		"time": "4:10 AM",
// 		"city": "Catacaos",
// 		"valid data": "Yes",
// 		"normaldist": "0.0538306598",
// 		"list": "9, 4"
// 	},
// 	{
// 		"id": 10,
// 		"date": "Sep 14, 2027",
// 		"time": "7:29 AM",
// 		"city": "Lauro de Freitas",
// 		"valid data": "No",
// 		"normaldist": -0.0881743447,
// 		"list": "8, 6, 2, 4, 1"
// 	},
// 	{
// 		"id": 11,
// 		"date": "Aug 3, 2026",
// 		"time": "4:05 AM",
// 		"city": "Tacoma",
// 		"valid data": "No",
// 		"normaldist": "0.3622162094",
// 		"list": "6, 9, 8, 4"
// 	},
// 	{
// 		"id": 12,
// 		"date": "Nov 13, 2025",
// 		"time": "8:01 AM",
// 		"city": "Cartagena",
// 		"valid data": "No",
// 		"normaldist": -0.3627613913,
// 		"list": "5, 7, 1, 10"
// 	},
// 	{
// 		"id": 13,
// 		"date": "Jul 19, 2027",
// 		"time": "9:55 PM",
// 		"city": "Culemborg",
// 		"valid data": "No",
// 		"normaldist": "0.4571934318",
// 		"list": "10, 1, 9"
// 	},
// 	{
// 		"id": 14,
// 		"date": "Nov 25, 2025",
// 		"time": "11:26 AM",
// 		"city": "Alacant",
// 		"valid data": "Yes",
// 		"normaldist": -0.0369198951,
// 		"list": "2, 3, 5"
// 	},
// 	{
// 		"id": 15,
// 		"date": "Sep 26, 2027",
// 		"time": "4:11 PM",
// 		"city": "İmamoğlu",
// 		"valid data": "Yes",
// 		"normaldist": -0.1353723663,
// 		"list": "5, 10, 7"
// 	}
// ]

const response = await fetch(props.dataUrl);
const { json: tableData } = await response.json();

const columns = Object.keys(tableData[0]).slice(0, 8);


const filteredData = computed(()=> {
    if (!searchTerm.value) {
        return tableData;
    };
    
    return tableData.filter((row : any) => {
        return columns.map((column) => row[column]).some((value) =>
        String(value).toLowerCase().includes(searchTerm.value.toLowerCase())
        );
    });
})

</script>

<template>
    <div class="bg-slate-700 rounded-lg px-8 py-4 m-5 space-y-4 flex flex-col justify-center items-center z-1 opacity-85 shadow-md max-h-9/10 max-w-45/100">
        <SearchField v-model="searchTerm" />
		<BasicTable :columns="columns" :tableData="filteredData">
		    <template v-for="column in columns" :key="column" #[`column-${column}`]="{ data }">
		        {{ data }}
		    </template>
	    </BasicTable>
	</div>
</template>