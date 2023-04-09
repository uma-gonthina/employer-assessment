<template>
    <div>
      <label
        for="assessment_id"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >assessment_id:</label
      >
      <div class="mt-2.5">
        <input
          name="assessment_id"
          v-model="form.assessment_id"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>
  
    <div>
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >recommendations:</label
      >
      <div class="mt-2.5">
        <input
          name="note"
          v-model="form.recommendations"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div>
      <label
        for="score"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >score:</label
      >
      <div class="mt-2.5">
        <input
        type="number"
          name="score"
          v-model="form.score"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div>
      <label
        for="attempt_count"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >attempt_count:</label
      >
      <div class="mt-2.5">
        <input
        type="number"
          name="attempt_count"
          v-model="form.attempt_count"
          id="note"
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
        @click="emit('add', form)"
        class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        save
      </button>
    </div>
  </template>
  <script setup lang="ts">
  const emit = defineEmits(["add", "cancel"]);
  const form = ref({
  "start_time": "2023-04-08T09:03:53",
  "end_time": "2023-04-08T09:03:53",
  "score": 0,
  "candidate_id": "3d022426500f4056959c0cc579838468",
  "assessment_id": "",
  "answers": {},
  "attempt_count": 0,
  "candidate_device": {},
  "recommendations": ""
});
  </script>
  