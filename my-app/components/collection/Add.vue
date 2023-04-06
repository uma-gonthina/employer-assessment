<template>
  <div >
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >name:</label
      >
      <div class="mt-2.5">
        <input
          name="note"
          v-model="form.name"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div >
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >difficulty_level:</label
      >
      <div class="mt-2.5">
        <input
          name="note"
          v-model="form.difficulty_level"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>

    <div >
      <label
        for="note"
        class="block text-sm font-semibold leading-6 text-gray-900"
        >description:</label
      >
      <div class="mt-2.5">
        <input
          name="note"
          v-model="form.description"
          id="note"
          rows="4"
          class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>
   
      <div class="mt-10">
        <button
          type="submit"
          @click="add()"
          class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          save
        </button>
      </div>
  
</template>
<script setup lang="ts">
const emit = defineEmits(["add"]);
const form = ref({
  "name": "",
  "type": "employer",
  "max_time_allowed": 0,
  "due_date": "2023-04-06T12:33:45.923Z",
  "difficulty_level": "",
  "description": "",
  "questions": {},
  "multiple_attempts_allowed": 0,
  "instructions": {},
  "status": 0,
  "owner_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "last_modified_date": "2023-04-06T12:33:45.923Z"
});
const add = () => {
  emit("add", form.value);
};
</script>
