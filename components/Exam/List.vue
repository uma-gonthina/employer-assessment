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


    <TransitionRoot appear :show="openModal" as="template">
        <Dialog as="div" @close="closeModal" class="relative z-10">
          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0"
            enter-to="opacity-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100"
            leave-to="opacity-0"
          >
            <div class="fixed inset-0 bg-black bg-opacity-25" />
          </TransitionChild>
    
          <div class="fixed inset-0 overflow-y-auto">
            <div
              class="flex min-h-full items-center justify-center p-4 text-center"
            >
              <TransitionChild
                as="template"
                enter="duration-300 ease-out"
                enter-from="opacity-0 scale-95"
                enter-to="opacity-100 scale-100"
                leave="duration-200 ease-in"
                leave-from="opacity-100 scale-100"
                leave-to="opacity-0 scale-95"
              >
                <DialogPanel
                  class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white p-6 text-left align-middle shadow-xl transition-all"
                >
                  <DialogTitle
                    as="h3"
                    class="text-lg font-medium leading-6 text-gray-900"
                  >
               {{edit?"Edit":"Delete"}}-Project
                  </DialogTitle>
    
                  <div v-if="edit">
                    <ExamEdit :project="editProject"
                              @edit="openModal = false,edit=false, emit('emitData', { note: $event, value: 'edit',index:editIndex })"
                              @cancel="closeModal" />
                  </div>
                  <div v-if="deleteProject">
                      <p>do you want to delete?</p>
                      <div class="mt-10 flex">
          <button
            type="submit"
            @click="openModal=false, emit('emitData', { note: $event, value: 'delete',index:editIndex })"
            class="block mr-2 rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            yes
          </button>
    
          <button
            type="submit"
            @click="closeModal"
            class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            no
          </button>
        </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
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
    "s_no",
    "name",
    "age",
    "gender",
    "date_of_birth",
    "designation",
  ]);
  const emit = defineEmits(["emitData"]);
  const props = defineProps({
    project: { type: Array, required: true },
  });
  const editProject = ref({})
 const editIndex=ref(-1);
  const edit = ref(false)

  const deleteProject = ref(false)

  const openModal=ref(false)


  const emitData = (note: any, index: any, value: any) => {
      openModal.value=true
      editIndex.value=index
      editProject.value = JSON.parse(JSON.stringify(note))
    if (value == 'edit') {
      edit.value = true
    }
    else{
        deleteProject.value=true
    }
  };
  const closeModal=()=>{
      openModal.value=false
      edit.value=false
      deleteProject.value=false
  }
  </script>