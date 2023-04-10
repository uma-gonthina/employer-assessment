<template>
  <div class="flex ml-3">
    <div class="relative w-[400px]">
      <div
        class="absolute inset-y-0 right-0 flex items-center pl-3 pointer-events-none"
      >
        <MagnifyingGlassIcon class="w-5 m-2" />
      </div>
      <input
        v-model="searchQuery"
        type="text"
        id="simple-search"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full pl-10 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        placeholder="Search name"
        required
        @input="getSearchName"
      />
    </div>
    <div class="ml-10 flex justify-end">
      <button
        type="button"
        class="rounded-full bg-indigo-600 p-4 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="openModal"
      >
        Add Employee
      </button>
    </div>
  </div>

  <div
    class="block w-full p-4 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
  >
    <ExamList
      v-if="employees && employees.length"
      :employee="employees"
      @emitData="emitData"
    />
  </div>

  <TransitionRoot appear :show="isOpen" as="template">
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
              </DialogTitle>

              <div>
                <ExamAdd @add="add" @cancel="isOpen = false"></ExamAdd>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup lang="ts">
import { ref } from "vue";
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
  DialogTitle,
} from "@headlessui/vue";

const isOpen = ref(false);

function closeModal() {
  isOpen.value = false;
}
function openModal() {
  isOpen.value = true;
}

const employees: any = ref([]);

onMounted(() => {
  if (localStorage.getItem("employeeDetails"))
    employees.value = JSON.parse(localStorage.getItem("employeeDetails"));
});

const add = async (employee: any) => {
  employees.value.push(employee);
  localStorage.setItem("employeeDetails", JSON.stringify(employees.value));

  isOpen.value = false;
};
// Edit employee
const edit = async (emp: any) => {
  employees.value[emp.index] = emp.emp;
  localStorage.setItem("employeeDetails", JSON.stringify(employees.value));
};
// Delete employee
const deleteEmployee = async (emp: any) => {
  employees.value.splice(emp.index, 1);
  localStorage.setItem("employeeDetails", JSON.stringify(employees.value));
};

// Edit and Delete events
const emitData = (emp: Object) => {
    emp.value == "edit" ? edit(emp) : deleteEmployee(emp);
};

const searchQuery = ref();

const getSearchName = () => {
  if (searchQuery.value) {
    employees.value = employees.value.filter((item: any) => {
      return item.name.toLowerCase().includes(searchQuery.value.toLowerCase());
    });
  } else {
    // If search query is empty, show all employees
    employees.value = JSON.parse(localStorage.getItem("employeeDetails"));
  }
};
</script>
