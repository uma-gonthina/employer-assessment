<template>
    <h1 class="font-bold ">Sales Details</h1>
<div class="flex justify-end">
       <button
         type="button"
         class="rounded-full bg-indigo-600 p-4 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
         @click="open = true"
       >
        ADD
       </button>
     </div>

   <div
     class="block w-[1200px] p-4 mr-2 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
   >
     <SalesList
       v-if="sales.length"
       :sales="sales"
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
                             >Sales-Information</DialogTitle
                           >
                           <div>
                             <SalesAdd
                               @add="add"
                               @cancel="open = false"
                             ></SalesAdd>
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
import { formatMessages } from "esbuild";
 const sales = ref([]);
 const { data:salesData } = await useAuthLazyFetch(
   `https://v2-orm-gharpe.mercury.infinity-api.net/api/leads/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
   {}
 );
 sales.value = salesData.value;
 const open = ref(false);
 const add = async (sales: any) => {
   const { data } = await useAuthLazyFetchPost(
     `https://v2-orm-gharpe.mercury.infinity-api.net/api/leads/`,
     {
       body: {
 "name": sales.name,
 "source": "GharPe",
 "phone_number": sales.phone_number,
 "email": sales.email,
 "status": sales.status,
 "purpose_of_buying": "Investment",
 "address": sales.address,
 "preferred_floor": 0,
 "facing": "string",
 "starred": true,
 "mode_of_payment": "Full Payment",
 "down_payment": "string",
 "is_loan_required": true,
 "cdata1": "string",
 "cdata2": "string",
 "project_id": "string"
},
     }
   );
   open.value = false;
   await getSalesDetails();
 };
 // Edit sales details
 const edit = async (sale: any) => {
   await useAuthLazyFetchPut(
     `https://v2-orm-gharpe.mercury.infinity-api.net/api/leads/${sale.sale.uid}`,
     {
       body: sale.sale,
     }
   );
   await getSalesDetails();
 };
 // Delete sales details
 const deleteSaleData = async (sale: any) => {
   await useAuthLazyFetchDelete(
     `https://v2-orm-gharpe.mercury.infinity-api.net/api/leads/${sale.sale.uid}`,
     {}
   );
   sales.value.splice(sale.index, 1);
 };
 // Edit and Delete events
 const emitData = (sale: Object) => {
   sale.value == "edit" ? edit(sale) : deleteSaleData(sale);
 };
 // Get sales details
 const getSalesDetails = async () => {
   const { data: salesData } = await useAuthLazyFetch(
     `https://v2-orm-gharpe.mercury.infinity-api.net/api/leads/?offset=0&limit=100&sort_column=id&sort_direction=desc`,
     {}
   );
   sales.value = salesData.value;
 };
 </script>