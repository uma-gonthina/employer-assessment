<template>
  <div>
    <label
      for="name"
      class="block text-sm font-semibold leading-6 text-gray-900"
      >name:</label
    >
    <div class="mt-2.5">
      <input
        name="name"
        v-model="sales.name"
        id="sale"
        rows="4"
        class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      />
    </div>
  </div>

  <div>
    <label
      for="status"
      class="block text-sm font-semibold leading-6 text-gray-900"
      >status:</label
    >
    <div class="mt-2.5">
      <select
        v-model="sales.status"
        class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      >
        <option
          v-for="(field, index) in status"
          :key="index"
          scope="col"
          class="py-3 5 pl-4 pr-3 text-left text-sm font-semibold sm:pl-0 group"
        >
          {{ field }}
        </option>
      </select>
    </div>
  </div>

  <div>
    <label
      for="phone_number"
      class="block text-sm font-semibold leading-6 text-gray-900"
      >phone_number:</label
    >
    <div class="mt-2.5">
      <input
        name="phone_number"
        v-model="sales.phone_number"
        id="sale"
        rows="4"
        class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      />
    </div>
  </div>

  <div>
    <label
      for="email"
      class="block text-sm font-semibold leading-6 text-gray-900"
      >email:</label
    >
    <div class="mt-2.5">
      <input
        name="email"
        v-model="sales.email"
        id="sale"
        rows="4"
        class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      />
    </div>
  </div>

  <div>
    <label
      for="address"
      class="block text-sm font-semibold leading-6 text-gray-900"
      >address:</label
    >
    <div class="mt-2.5">
      <input
        name="address"
        v-model="sales.address"
        id="sale"
        rows="4"
        class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      />
    </div>
  </div>

  <div class="mt-10 flex">
    <button
      type="submit"
      @click="emit('cancel')"
      class="block mr-2 rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
    >
      cancel
    </button>

    <button
      type="submit"
      @click="emit('edit', sales)"
      class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
    >
      update
    </button>
  </div>
</template>
<script setup lang="ts">
interface sales {
  sales: {
    name: string;
    source: "GharPe";
    phone_number: string;
    email: string;
    status: "Active";
    purpose_of_buying: "Investment";
    address: string;
    preferred_floor: 0;
    facing: string;
    starred: true;
    mode_of_payment: "Full Payment";
    down_payment: string;
    is_loan_required: true;
    cdata1: string;
    cdata2: string;
    project_id: string;
  };
}
const props = defineProps<sales>();
const sales = ref(props.sales);

const status = ref([
  "Active",
  "Interested",
  "Hot Interest",
  "Not Interested",
  "Closed",
]);

// Close input after editing
const emit = defineEmits(["edit", "cancel"]);
</script>
