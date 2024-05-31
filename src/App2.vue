<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue';
import post from '@/components/listing.vue';
import focused_post from '@/components/Post.vue';
let items = [2, 8, 9 ,2];

const sidebar_posts = ref({})
let last_id = ref("")
update_posts()
async function update_posts() {
  let posts;
  await fetch(import.meta.env.VITE_BACKEND_URL + "forum/", {
    method:"get",
    credentials:"omit",
    mode:"cors",
    //headers: {"page_amount":4}
  }).then((response) => response.json().then((objects)=>sidebar_posts.value=objects))
}
function focus_post(id) {
  last_id.value = id;
}
</script>
<template>
  <focused_post :post_id="last_id"/>
        <nav >
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/about">About</RouterLink>
            <RouterLink to="/forum">Forum</RouterLink>
            <RouterLink to="/newpost">Create New Listing</RouterLink>
        </nav>
    <aside class="box">
        <RouterView @openPost="(id)=>focus_post(id)" class="main"/>
        <div class="sidebar">
        <!--    <post v-for="post in sidebar_posts" :difficulty="post.challange" :title="post.title" :discription="post.body"/>  -->
      </div>
    </aside>
</template>


<style scoped>
nav {
    display: flex;
    font-size: 20px;
    flex-flow: row nowrap;
    justify-content: end;
}

.box{
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-areas: "main sidebar";
    
}

.sidebar {
    grid-area: sidebar;
    margin: 0px 1rem;
}
.main{
    grid-area: main;
    margin: 0px 1rem;

}
nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav :first-of-type {
  border: 0;
}

</style>