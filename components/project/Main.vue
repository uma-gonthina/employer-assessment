<template>
  <div
    class="block w-full p-4 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
  >
    <div class="flex justify-end">
      <button
        type="button"
        class="rounded-full bg-indigo-600 p-4 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="open = true"
      >
        New project
      </button>
    </div>
    <projectList
      v-if="project.length"
      :project="project"
      @emitData="emitData"
    />
  </div>
  <div class="flex justify-end">
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
                            >Add-Project</DialogTitle
                          >
                          <div>
                            <projectAdd
                              @add="add"
                              @cancel="open = false"
                            ></projectAdd>
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

const project = ref([]);

const editInput = ref([]);

const { data: projectdata } = await useAuthLazyFetch(
  `https://v2-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
  {}
);
project.value = projectdata.value;

const open = ref(false);

const add = async (project: any) => {
  const { data } = await useAuthLazyFetchPost(
    `https://v2-orm-gharpe.mercury.infinity-api.net/api/projects/`,
    {
      body: {
        name: project.name,
        listing_type_name: project.listing_type_name,
        category: project.category,
        sub_category: "Apartment",
        status: project.status,
        details: project.details,
        specifications: project.specifications,
        possession_date: "2023-04-08",
        age_of_the_project: "string",
        logo_url: "string",
        total_project_area: 0,
        metric: "sq.ft",
        default_image_url: "string",
        visit_count: 0,
        rera_approved: true,
        approve_status: project.approve_status,
      },
    }
  );
  open.value = false;
  await getProjects();
};

// Edit notes
const edit = async (note: any) => {
  await useAuthLazyFetchPut(
    `https://v2-orm-gharpe.mercury.infinity-api.net/api/projects/${note.note.uid}`,
    {
      body: note.note,
    }
  );
  await getProjects();
};

// Delete Projects
const deleteNote = async (note: any) => {
  await useAuthLazyFetchDelete(
    `https://v2-orm-gharpe.mercury.infinity-api.net/api/projects/${note.note.uid}`,
    {}
  );
  project.value.splice(note.index, 1);
};

// Edit and Delete events
const emitData = (note: Object) => {
  note.value == "edit" ? edit(note) : deleteNote(note);
};

// Get Projects
const getProjects = async () => {
  const { data: projectdata } = await useAuthLazyFetch(
    `https://v2-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
    {}
  );
  project.value = projectdata.value;
};
</script>
