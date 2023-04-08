<template>
    <div
      class="block w-[800px] p-4 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
    >
      <ApplicationsList v-if="application.length" :application="application" />
    </div>
    <div class="flex justify-end">
      <button
        type="button"
        class="rounded-full bg-indigo-600 p-4 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="open = true"
      >
        Add Application
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
                              <ApplicationsAdd
                                @add="add"
                                @cancel="open = false"
                              ></ApplicationsAdd>
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
  
  const application = ref([]);
  
  const { data:appplicationData } = await useAuthLazyFetch(
    `https://v7-stark-db-orm.mercury.infinity-api.net/api/assessments/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
    {}
  );
  application.value = appplicationData.value;
  
  const open = ref(false);
  
  const add = async (application: any) => {
    const { data } = await useAuthLazyFetchPost(
      `https://v7-stark-db-orm.mercury.infinity-api.net/api/applications/`,
      {
        body: {
  "candidate_id": application.candidate_id,
  "job_posting_id": "string",
  "status": application.status,
  "resume_url": application.resume_url,
  "cover_letter": application.cover_letter,
  "track_info": [],
  "questionnaire": []
},
      }
    );
    open.value = false;
    getApplications();
  };
  
  // Get forms
  const getApplications = async () => {
    application.value = [];
    const { data: appplicationData } = await useAuthLazyFetch(
      `https://v7-stark-db-orm.mercury.infinity-api.net/api/assessments/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
      {}
    );
    application.value = appplicationData.value;
  };
  
  //
  
  // };
  </script>
  