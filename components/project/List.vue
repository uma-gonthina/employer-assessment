<template>
  <table class="min-w-full divide-y divide-gray-700">
    <thead>
      <tr>
        <th
          v-for="(field, index) in fields"
          :key="index"
          scope="col"
          class="py-3 5 pl-4 pr-3 text-left text-sm font-semibold sm:pl-0 group"
        >
          {{ field }}
        </th>
      </tr>
    </thead>
    <tbody class="divide-y divide-gray-800">
      <tr
        v-for="(row, index) in project"
        :key="`item-${index}`"
        class="cursor-pointer hover:bg-gray-200"
      >
        <td
          v-for="(field, index) in fields"
          :key="`row-${index}`"
          class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium sm:pl-0"
        >
          {{ row[field] }}
        </td>
        <div class="flex">
          <TrashIcon class="w-7 m-3" @click="emitData(row, index, 'delete')"/>
          <PencilSquareIcon
            class="w-7 m-3"
            @click="emitData(row, index, 'edit')"
          />
        </div>
      </tr>
    </tbody>
  </table>
</template>
<script setup lang="ts">
import { TrashIcon, PencilSquareIcon } from "@heroicons/vue/24/outline";

const fields = ref([
  "name",
  "status",
  "listing_type_name",
  "details",
  "approve_status",
]);
const emit = defineEmits(["emitData"]);
const props = defineProps({
  project: { type: Array, required: true },
});
const emitData = (note: any, index: any, value: any) => {
   
  emit("emitData", { note: note, value: value, index: index });
};
</script>
