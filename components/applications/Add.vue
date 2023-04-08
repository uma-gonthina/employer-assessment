<template>
    <div>
      <label
        for="application"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >candidate_id:</label
      >
      <div class="mt-2.5">
        <input
          name="application"
          v-model="application.candidate_id"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>
  
    <div>
      <label
        for="application"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >status:</label
      >
      <div class="mt-2.5">
        <select
          v-model="application.status"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        >
          <option>Applied</option>
          <option>Disqualified</option>
          <option>Shortlisted</option>
          <option>Rejected</option>
        </select>
      </div>
    </div>
  
    <div>
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >cover_letter:</label
      >
      <div class="mt-2.5">
        <input
          name="application"
          v-model="application.cover_letter"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>
  
    <div>
      <label
        for="application"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >resume_url:</label
      >
      <div class="mt-2.5">
        <input
          name="application"
          v-model="application.resume_url"
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
        @click="emit('add', application)"
        class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        save
      </button>
    </div>
  </template>
  <script setup lang="ts">
  const emit = defineEmits(["add", "cancel"]);
  const application = ref({
  "candidate_id": " ",
  "job_posting_id": "string",
  "status": "Applied",
  "resume_url": " ",
  "cover_letter": " ",
  "track_info": [],
  "questionnaire": []
});
  </script>
  