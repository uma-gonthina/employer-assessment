<template>
  <table class="min-w-full divide-y divide-gray-700">
    <thead>
      <tr>
        <th v-for="(field, index) in fields" :key="index" scope="col"
          class="py-3 5 pl-4 pr-3 text-left text-sm font-semibold sm:pl-0 group">
          {{ field }}
        </th>
      </tr>
    </thead>
    <tbody class="divide-y divide-gray-800">
      <tr v-for="(row, index) in project" :key="`item-${index}`" class="cursor-pointer hover:bg-gray-200">
        <td v-for="(field, index) in fields" :key="`row-${index}`"
          class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium sm:pl-0">
          {{ row[field] }}
        </td>
        <div class="flex">
          <TrashIcon class="w-7 m-3" @click="emitData(row, index, 'delete')" />
          <PencilSquareIcon class="w-7 m-3" @click="emitData(row, index, 'edit')" />
        </div>
      </tr>
    </tbody>
  </table>
  <TransitionRoot as="template" :show="edit">
    <Dialog as="div" class="relative z-10" @close="edit = false">
      <div class="fixed inset-0" />


      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10">
            <TransitionChild as="template" enter-from="translate-x-full" enter-to="translate-x-0"
              leave-from="translate-x-0" leave-to="translate-x-full">
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <div class="flex h-full flex-col divide-y divide-gray-200 bg-white shadow-xl">
                  <div class="flex min-h-0 flex-1 flex-col overflow-y-scroll py-6">
                    <div class="px-4 sm:px-6">
                      <div>
                        <DialogTitle class="text-base font-semibold leading-6 text-gray-900">Edit-Project</DialogTitle>
                        <div>
                          <ProjectEdit :project="editProject"
                            @edit="edit = false, emit('emitData', { note: $event, value: 'edit' })"
                            @cancel="edit = false" />
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
<script setup lang="ts">
import {
  TransitionChild,
  DialogPanel,
  TransitionRoot,
  Dialog,
} from "@headlessui/vue";
import { TrashIcon, PencilSquareIcon } from "@heroicons/vue/24/outline";


const fields = ref([
  "name",
  "status",
  "listing_type_name",
  "approve_status",
]);
const emit = defineEmits(["emitData"]);
const props = defineProps({
  project: { type: Array, required: true },
});
const editProject = ref({})
const edit = ref(false)
const emitData = (note: any, index: any, value: any) => {
  if (value == 'edit') {
    editProject.value = JSON.parse(JSON.stringify(note))
    edit.value = true
    return;
  }
  emit("emitData", { note: note, value: value, index: index });
};
</script>