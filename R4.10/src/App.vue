<script setup>
import postCard from "@/components/postCard.vue";
import { computed, ref } from "vue";
const posts = ref([]);
const sortedPosts = computed(() => posts.value.toSorted((a, b) => b.computed));

const text = ref("");
const trimmedText = computed(() => text.value.trim());

function deletePost(id) {
  posts.value = posts.value.filter((post) => post.id !== id);
}

function likePost(id) {
  const postUpdate = posts.value.find((post) => post.id == id);
  postUpdate.like = !postUpdate.like;
  //posts.find((post) => post.id == id).like++;
}

function addPost() {
  const newPost = {
    id: Math.random().toString(36).substring(2),
    content: text.value.trim(),
    createdAt: new Date(),
    author: {
      username: "Camou",
      avatarUrl: "https://media1.tenor.com/m/a5RGfluwSOgAAAAd/sylvian-delhoumi.gif",
    },
    like: false,
  };
  posts.value.push(newPost);

  text.value = "";
}
</script>

<template>
  <RouterView />
</template>
