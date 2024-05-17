<template>
  <div class="flex flex-col w-full">
    <Header @search-title="searchTitle" />
    <div class="rounded-full grid grid-cols-1 gap-5 p-5 sm:grid-cols-3">
      <div
        class="bg-stone-200 flex p-5 items-center"
        @click="goNextPage(p.id)"
        v-for="p in postFilter()"
        :key="p.id"
        :v-if="post"
      >
        <posts :id="p.id" :title="titleSub[p.id - 1]" />
      </div>
    </div>
  </div>
</template>

<script setup>
import Header from "@/components/Header.vue";
import posts from "@/components/posts.vue";
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";

const title1 = ref("");
function searchTitle(t) {
  title1.value = t;
  console.log(title1.value);
}

const router = useRouter();

function goNextPage(postid) {
  router.push(`posts/${postid}`);
}

const post = ref([]);
const titleSub = ref([]);
const f = async () => {
  try {
    const data = await fetch("https://jsonplaceholder.typicode.com/posts");
    const response = await data.json();
    response.forEach((element, index) => {
      post.value.push(element);
      titleSub.value[index] = element.title.substring(0, 20);
    });
  } catch (err) {
    console.log(err);
  }
};

onMounted(async () => {
  await f();
});

const postFilter = () => {
  return post.value.filter((p) => p.title.includes(title1.value.toLowerCase()));
};
</script>
