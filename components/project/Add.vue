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
          v-model="project.name"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div>
      <label
        for="category"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >category:</label
      >
    <div class="mt-2.5">
        <select
          v-model="project.category"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        >
          <option>Residential</option>
          <option>Commercial</option>
        </select>
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
          v-model="project.status"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        >
          <option>Fully Constructed</option>
          <option>Under Construction</option>
          <option>New Venture</option>
        </select>
      </div>
    </div>
  
    <div>
      <label
        for="listing_type_name"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >listing_type_name:</label
      >
      <div class="mt-2.5">
        <input
          name="listing_type_name"
          v-model="project.listing_type_name"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>
  
    <div>
      <label
        for="details"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >details:</label
      >
      <div class="mt-2.5">
        <input
          name="details"
          v-model="project.details"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div>
      <label
        for="specifications"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >specifications:</label
      >
      <div class="mt-2.5">
        <input
          name="specifications"
          v-model="project.specifications"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

<div>
      <label
        for="approve_status"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >approve_status:</label
      >
    <div class="mt-2.5">
        <select
          v-model="project.approve_status"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        >
          <option>Under Review</option>
          <option>Rejected</option>
          <option>Active</option>
          <option>Deleted</option>
          <option>Expiring Soon</option>
          <option>Expired</option>
          <option>Inactive</option>
        </select>
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
        @click="emit('add', project)"
        class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        save
      </button>
    </div>
  </template>
  <script setup lang="ts">
  const emit = defineEmits(["add", "cancel"]);
  const project = ref({
  "name": "",
  "listing_type_name": "",
  "category": "Residential",
  "sub_category": "Apartment",
  "status": "Fully Constructed",
  "details": "",
  "specifications": "",
  "possession_date": "2023-04-08",
  "age_of_the_project": "string",
  "logo_url": "string",
  "total_project_area": 0,
  "metric": "sq.ft",
  "default_image_url": "string",
  "visit_count": 0,
  "rera_approved": true,
  "approve_status": "Active"
});
  </script>
  