<script setup>
defineProps({
  post: {
    type: Object,
    required: true,
  },
});
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
        <button>Supprimer</button>
    </footer>
  </article>
</template>
