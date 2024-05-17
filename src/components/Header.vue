<template>
  <div class="h-52 bg-yellow-600 flex justify-center items-center">
    <div class="flex bg-white p-4 rounded-full">
      <input
        @input="search"
        v-model="inputName"
        type="text"
        class="w-72 focus:outline-none ml-2"
        placeholder="search posts"
      />
      <button class="border-solid" @click="search">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z"
          />
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const inputName = ref("");

const emit = defineEmits(["searchTitle"]);

function search() {
  emit("searchTitle", inputName.value);
}
</script>

<style></style>
