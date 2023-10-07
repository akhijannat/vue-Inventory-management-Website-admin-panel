<script setup>
import { RouterLink, RouterView } from "vue-router";
import axios from "axios";
import { ref, onBeforeMount, reactive } from "vue";
import { useProduct } from "../stores/productStore.js";
import { storeToRefs } from "pinia";

const pro = useProduct();

const { products, singleProduct } = storeToRefs(pro);

onBeforeMount(() => {
  pro.getData();
});

const detailsBtn =
  "text-right border border-lime-600 font-semibold transition duration-200 rounded-sm py-1 px-3 text-lime-600 hover:shadow-xl";

const Header = [
  { text: "Category", value: "category" },
  { text: "Brand", value: "brand" },
  { text: "Image", value: "thumbnail" },
  { text: "Name", value: "title", sortable: true },
  { text: "Price (Tk)", value: "price", sortable: true },
  { text: "Stock", value: "stock" },
  { text: "Rating", value: "img " },
  { text: "Action", value: "id" },
];

function itemView(id) {
  pro.getSingleProductDetails(id);
}

const searchField = [
  "Category",
  "Brand",
  "Image",
  "Name",
  "Price",
  "Stock",
  "Rating",
];

const searchValue = ref();
</script>
<template>
  <div class="container mx-auto my-5">
    <h6 class="text-4xl pb-2 text-center">Products</h6>
    <div class="h-1 bg-slate-600 w-52 mx-auto my-3"></div>

    <div class="w-1/2 mx-auto mt-10 mb-5">
      <input
        placeholder="Search..."
        class="p-2 w-full border rounded focus:outline-none focus:bg-slate-200"
        id="inline-full-name"
        type="text"
        v-model="searchValue"
      />
    </div>

    <EasyDataTable
      :headers="Header"
      :items="products"
      :rows-per-page="10"
      :search-field="searchField"
      :search-value="searchValue"
    >
      <template #item-thumbnail="{ thumbnail }">
        <img :src="thumbnail" alt="" class="custom" />
      </template>

      <template #item-id="{ id }">
        <button
          class="translate duration-300 hover:scale-110"
          @click="itemView(id)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="black"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z"
            />
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
            />
          </svg>
        </button>
      </template>
    </EasyDataTable>
  </div>
</template>

<style scoped>
.custom {
  height: 60px;
  width: 60px;
}
</style>
