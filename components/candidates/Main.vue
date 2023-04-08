<template>
    <div
      class="block w-[800px] p-4 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
    >
      <CandidatesList v-if="candidate.length" :candidate="candidate" />
    </div>
    <div class="flex justify-end">
      <button
        type="button"
        class="rounded-full bg-indigo-600 p-4 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="open = true"
      >
        ADD
      </button>
      <TransitionRoot as="template" :show="open">
        <Dialog as="div" class="relative z-10" @close="open = false">
          <div class="fixed inset-0" />
  
          <div class="fixed inset-0 overflow-hidden">
            <div class="absolute inset-0 overflow-hidden">
              <div
                class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
              >
                <TransitionChild
                  as="template"
                  enter-from="translate-x-full"
                  enter-to="translate-x-0"
                  leave-from="translate-x-0"
                  leave-to="translate-x-full"
                >
                  <DialogPanel class="pointer-events-auto w-screen max-w-md">
                    <div
                      class="flex h-full flex-col divide-y divide-gray-200 bg-white shadow-xl"
                    >
                      <div
                        class="flex min-h-0 flex-1 flex-col overflow-y-scroll py-6"
                      >
                        <div class="px-4 sm:px-6">
                          <div>
                            <DialogTitle
                              class="text-base font-semibold leading-6 text-gray-900"
                              >Add-Candidate</DialogTitle
                            >
                            <div>
                              <CandidatesAdd
                                @add="add"
                                @cancel="open = false"
                              ></CandidatesAdd>
                            </div>
  
                            <div class="ml-3 flex h-7 items-center">
                              <button
                                type="button"
                                class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500"
                                @click="open = false"
                              >
                                <span class="sr-only">Close panel</span>
                                <XMarkIcon aria-hidden="true" />
                              </button>
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
    </div>
  </template>
  <script setup lang="ts">
  import {
    TransitionChild,
    DialogPanel,
    TransitionRoot,
    Dialog,
  } from "@headlessui/vue";
  import { PlusIcon, XMarkIcon } from "@heroicons/vue/24/outline";
  
  const candidate = ref([]);
  
  const { data: candidateData } = await useAuthLazyFetch(
    `https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/?offset=0&limit=100&sort_column=id&sort_direction=desc
`,
    {}
  );
  candidate.value = candidateData.value;
  
  const open = ref(false);
  
  const add = async (candidate: any) => {
    const { data } = await useAuthLazyFetchPost(
      `https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/`,
      {
        body: {
  "name": candidate.name,
  "type": candidate.type,
  "max_time_allowed": 0,
  "due_date": "2023-04-08T07:07:33.771Z",
  "difficulty_level": candidate.difficulty_level,
  "description": candidate.description,
  "questions": {},
  "multiple_attempts_allowed": 0,
  "instructions": {},
  "status": 0,
  "owner_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "last_modified_date": "2023-04-08T07:07:33.771Z"
},
      }
    );
    open.value = false;
    getCandidates();
  };
  
  // Get forms
  const getCandidates = async () => {
    candidate.value = [];
    const { data: candidateData } = await useAuthLazyFetch(
      `https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/?offset=0&limit=100&sort_column=id&sort_direction=desc
`,
      {}
    );
    candidate.value = candidateData.value;
  };
  
  //
  
  // };
  </script>
  