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
  posts.find((post) => post.id == id).like++;
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
    like: 0,
  };
  posts.value.push(newPost);

  text.value = "";
}
</script>

<template>
  <main>
    <div class="container">
      <form class="card" @submit.prevent="addPost">
        <textarea name="post" id="post" placeholder="saissiez" v-model="text"></textarea>
        <button type="submit" :disabled="!text.trim()">Publier</button>
      </form>
      <h2 v-if="!posts.length">Aucun posts</h2>

      <postCard
        v-for="(post, index) in sortedPosts"
        :key="index"
        :post="post"
        @delete="deletePost"
        @like="likePost"
      />
      <!--
      <article class="card" v-for="(post, index) in sortedPosts" :key="index">
        <header>
          <img :src="post.author.avatarUrl" alt="avatar" width="36" height="36" />
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
      </article>
      -->
    </div>
  </main>
</template>
