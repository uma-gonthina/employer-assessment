<template>
    <div>
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >name:</label
      >
      <div class="mt-2.5">
        <input
          name="name"
          v-model="candidate.name"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div>
      <label
        for="type"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >type:</label
      >
      <div class="mt-2.5">
        <select
          v-model="candidate.type"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        >
          <option> practice</option>
          <option>videoprofile</option>
        </select>
      </div>
    </div>
  
    <div>
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >difficulty_level:</label
      >
      <div class="mt-2.5">
        <select
          v-model="candidate.difficulty_level"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        >
          <option>Easy</option>
          <option>Medium</option>
          <option>Hard</option>
        </select>
      </div>
    </div>
  
    <div>
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >description:</label
      >
      <div class="mt-2.5">
        <input
          name="description"
          v-model="candidate.description"
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
        >Due Date:</label
      >
      <div class="mt-2.5">
        <input
          name="due_date"
          type="date"
          v-model="candidate.due_date"
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
        @click="emit('add', candidate)"
        class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        save
      </button>
    </div>
  </template>
  <script setup lang="ts">
  const emit = defineEmits(["add", "cancel"]);
  const candidate = ref({
  "name": "",
  "type": "practice",
  "max_time_allowed": 0,
  "due_date": "2023-04-08T07:07:33.771Z",
  "difficulty_level": "Easy",
  "description": "",
  "questions": {},
  "multiple_attempts_allowed": 0,
  "instructions": {},
  "status": 0,
  "owner_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "last_modified_date": "2023-04-08T07:07:33.771Z"
});
  </script>
  