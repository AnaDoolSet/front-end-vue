<script setup lang="ts">
const props = defineProps({
  columns: {
    type: Array as () => string[],
    required: true
  },
  tableData: {
    type: Array as () => Record<string, any>[],
    required: true
  }
});

</script>

<template>
    <span class="overflow-auto rounded-sm" style="width: stretch">
        <table class="table table-auto border-collapse border border-zinc-200 text-zinc-50 w-max">
            <thead>
                <tr>
                    <th v-for="column in columns" :key="column" class="border border-zinc-200 px-4 py-2 bg-slate-500 w-1/20">
                        {{ column }}
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="data in props.tableData" :key="data.id">
                    <td v-for="column in columns" :key="`${column}-${data.id}`" class="border border-zinc-200 px-4 py-2 bg-slate-400" :class="{'max-w-3xs break-words': String(data[column] ?? '').length > 30}">
                        <slot :name="`column-${column}`" :data="data[column]"></slot>
                    </td>
                </tr>
            </tbody>
        </table>
    </span>
</template>