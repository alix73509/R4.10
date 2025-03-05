<script setup>
import { TrashIcon } from "@heroicons/vue/24/outline";
import { HeartIcon } from "@heroicons/vue/24/outline";
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

const sortedPosts = [];
</script>

<template>
  <article class="card">
    <header>
      <img :src="post.author.avatarUrl" alt="avatar" width="36" height="36" class="avatar" />
      <a>{{ post.author.username }}</a>
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
        <HeartIcon />
      </button>
      <p>{{ post.like }}</p>
    </footer>
  </article>
</template>
