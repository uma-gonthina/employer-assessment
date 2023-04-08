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
        v-for="(row, index) in candidate"
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
      </tr>
    </tbody>
  </table>
</template>
<script setup>
const fields = ref(["name","type", "difficulty_level", "description"]);
const props = defineProps({
candidate: { type: Array, required: true },
});
</script>
