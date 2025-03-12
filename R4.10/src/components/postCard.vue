<script setup>
import { TrashIcon } from "@heroicons/vue/24/outline";
import { HeartIcon } from "@heroicons/vue/24/outline";
import { HeartIcon as SolidHeartIcon } from "@heroicons/vue/24/solid";
import { useRouter } from "vue-router";

const router = useRouter();

const props = defineProps({
  post: {
    type: Object,
    required: true,
  },
});
const emit = defineEmits(["delete", "like"]);

function deletePost() {
  emit("delete", props.post.id);
}

function likePost() {
  emit("like", props.post.id);
}

function goToUserProfile() {
  router.push({ name: "user", params: {username: props.post.author.username} });
}

const sortedPosts = [];
</script>

<template>
  <article class="card">
    <header>
      <img :src="post.author.avatarUrl" alt="avatar" width="36" height="36" class="avatar" />
      <a @click="goToUserProfile">{{ post.author.username }}</a>
      <b>
        {{
          post.createdAt.toLocaleString("fr-FR", {
            weekday: "long",
            year: "numeric",
            month: "long",
            day: "numeric",
            hour: "2-digit",
            minute: "2-digit",
            second: "2-digit",
          })
        }}
      </b>
    </header>
    <p>{{ post.content }}</p>

    <footer>
      <button @click="deletePost" class="btn-icon">
        <TrashIcon />
      </button>

      <button @click="likePost" class="btn-icon">
        <HeartIcon v-if="!post.like" />
        <SolidHeartIcon v-else class="active" />
      </button>
    </footer>
  </article>
</template>
