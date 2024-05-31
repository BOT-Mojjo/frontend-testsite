<script setup>
import { ref } from 'vue';
import Post from '@/components/listing.vue';
let disc="mmmm mm m m mmmmmmmmm mmmmm mm mmmmmm mmm mmmmmmmmm mmmm mmmmm"
const sidebar_posts = ref({})
let last_id = 0
update_posts()
async function update_posts() {
  let posts;
  await fetch(import.meta.env.VITE_BACKEND_URL + "forum/", {
    method:"get",
    credentials:"omit",
    mode:"cors",
    // headers:{'page_amount':4}
  }).then((response) => response.json().then((objects)=>sidebar_posts.value=objects))
}
</script>

<template>
    <div>
      <post @click="$emit('openPost', post._id)"v-for="post in sidebar_posts" :difficulty="post.challange" :title="post.title" :discription="post.body"/>
    </div>
</template>
  
  <style>
  @media (min-width: 1024px) {
    .about {
      min-height: 100vh;
      display: flex;
      align-items: center;
    }
  }
  </style>