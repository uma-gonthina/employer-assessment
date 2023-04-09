<template>
    <div
      class="block w-[800px] p-4 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
    >
      <CandidateresponsesList v-if="form.length" :form="form" />
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
                              >Candidate Information</DialogTitle
                            >
                            <div>
                              <CandidateresponsesAdd
                                @add="add"
                                @cancel="open = false"
                              ></CandidateresponsesAdd>
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
  
  const form = ref([]);
  
  const { data: formdata } = await useAuthLazyFetch(
    `https://v7-stark-db-orm.mercury.infinity-api.net/api/responses/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
    {}
  );
  form.value = formdata.value;
  
  const open = ref(false);
  
  const add = async (form: any) => {
    const { data } = await useAuthLazyFetchPost(
      `https://v7-stark-db-orm.mercury.infinity-api.net/api/responses/`,
      {
        body: {
  "start_time": "2023-04-08T09:03:53",
  "end_time": "2023-04-08T09:03:53",
  "score": form.score,
  "candidate_id": "3d022426500f4056959c0cc579838468",
  "assessment_id": form.assessment_id,
  "answers": {},
  "attempt_count": form.attempt_count,
  "candidate_device": {},
  "recommendations": form.recommendations
},
      }
    );
    open.value = false;
    candidateResponses();
  };
  
  // Get candidateResponses
  const candidateResponses = async () => {
    form.value = [];
    const { data: formdata } = await useAuthLazyFetch(
      `https://v7-stark-db-orm.mercury.infinity-api.net/api/responses/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
      {}
    );
    form.value = formdata.value;
  };
  
  //
  
  // };
  </script>