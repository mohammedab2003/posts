<template>
  <div
    v-if="post == null && comments == null"
    class="w-full gap-x-2 flex justify-center items-center h-full"
  >
    <div
      class="w-[48px] h-[48px] m-auto relative before:content-[''] before:w-[48px] before:h-[5px] before:bg-[#f0808050] before:absolute before:top-[60px] before:left-[0px] before:rounded-[50%] before:animate-[shadow324_0.5s_linear_infinite] after:content-[''] after:w-[100%] after:h-[100%] after:bg-[#f08080] after:absolute after:top-[0px] after:left-[0px] after:rounded-[4px] after:animate-[jump7456_0.5s_linear_infinite]"
    ></div>
  </div>
  <div
    class="flex flex-col sm:gap-y-10 w-full sm:flex-row"
    v-if="post != null && comments != null"
  >
    <div
      class="sm:m-20 sm:rounded-3xl sm:border-none border-b-2 border-black bg-orange-100 p-5 flex flex-col w-full sm:w-1/3"
    >
      <span class="text-blue-500 text-3xl p-5">details</span>
      <span class="p-3">user id is : {{ post.userId }}</span>
      <span class="p-3">id of the post is : {{ post.id }}</span>
      <span class="p-3">body of post is { {{ post.body }} }</span>
      <button
        class="p-3 bg-blue-600 text-2xl text-white rounded-full sm:mt-10"
        @click="back"
      >
        back to Home
      </button>
    </div>

    <div class="sm:m-20 bg-orange-100 sm:rounded-3xl sm:w-2/3 py-5 px-20">
      <span v-if="show" class="text-3xl p-5 text-blue-500">comments</span>
      <span v-if="!show" class="text-3xl p-5 text-blue-500"
        >the required comment</span
      >
      <div v-if="show">
        <div
          v-for="comment in comments"
          :key="comment.id"
          @click="showComment(comment)"
          class="my-2"
        >
          <div
            class="flex p-5 items-center border-black border-solid border-b-2"
          >
            <span class="rounded-md bg-white p-3">{{ comment.id }}</span>
            <span class="p-3 text-xl mx-auto"> {{ comment.name }}</span>
          </div>
        </div>
      </div>
      <div v-if="!show && cm != null" class="my2 flex flex-col items-start">
        <span class="p-3 border-black border-solid border-b-2"
          >post id of this comment is : {{ cm.postId }}</span
        >
        <span class="p-3 border-black border-solid border-b-2">
          Id of this comment is : {{ cm.id }}</span
        >
        <span class="p-3 border-black border-solid border-b-2">
          Name of this comment is : {{ cm.name }}</span
        >
        <span class="p-3 border-black border-solid border-b-2">
          Email of this comment is : {{ cm.email }}</span
        >
        <span class="p-3"> Body of this comment is : {{ cm.body }} </span>
        <button
          class="p-3 bg-blue-600 text-2xl text-white rounded-full"
          @click="show = !show"
        >
          back to comments
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
const router = useRouter();
const route = useRoute();

const back = () => {
  router.back();
};

const post = ref(null);
const comments = ref(null);
const show = ref(true);

const f = async () => {
  try {
    const postt = await fetch(
      `https://jsonplaceholder.typicode.com/posts/${route.params.id}`
    );

    const commentts = await fetch(
      `https://jsonplaceholder.typicode.com/comments?postId=${route.params.id}`
    );

    const postResponse = await postt.json();
    const commentResponse = await commentts.json();
    post.value = postResponse;
    comments.value = commentResponse;
  } catch (err) {
    console.log(err);
  }
};

onMounted(async () => {
  await f();
});
const cm = ref(null);
const showComment = (c) => {
  show.value = !show.value;
  cm.value = c;
};
</script>

<style></style>
