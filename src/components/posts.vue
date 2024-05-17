<template>
  <span class="rounded-md bg-white p-3">{{ id }}</span>
  <span class="p-3 text-xl mx-auto"> {{ title }}</span>
</template>

<script setup>
const props = defineProps({ id: Number, title: String });
const id = props.id;
const title = props.title;
</script>

<style></style>
