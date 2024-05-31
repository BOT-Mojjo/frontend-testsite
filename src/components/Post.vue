<script setup>
import { ref, watch } from 'vue';
import listing from './listing.vue';

const dialog = ref(null)
const props = defineProps(["post_id"])
const post = ref({})

watch(props, (new_post)=>get_post(new_post.post_id))
watch(post, ()=>{dialog.value.showModal()})

async function get_post(id){
    if (id == 0) return;
    await fetch(import.meta.env.VITE_BACKEND_URL + "post/" + id, {
    method:"get",
    credentials:"omit",
    mode:"cors"
    }).then((tea) => tea.json().then((tea2) => post.value = tea2))
}

async function delete_post(id){
    let a =await fetch(import.meta.env.VITE_BACKEND_URL + "post/" + id,  {
        method:"delete",
        credentials:"omit",
        mode:"cors"
    })
}

async function bump_post(id){
    let a = await fetch(import.meta.env.VITE_BACKEND_URL + "post/" + id,  {
        method:"post",
        credentials:"omit",
        mode:"cors"
    }).then((tea) => tea.json().then((tea2) => post.value.post_rating = tea2))
}

</script>

<template>
    <dialog ref="dialog">
        <article class="focused">
            <listing :difficulty="post.challange" :title="post.title" :discription="post.body"/>
            <nav>
                <button @click="bump_post(post._id)">Bump</button>
                <button @click="delete_post(post._id); dialog.close()">Delete</button>
                <button @click="dialog.close()">Close</button>
                <p style ="width:1rem;">{{ post.post_rating }}</p>
            </nav>
        </article>
    </dialog>
</template>

<style scoped>


nav {
    display: flex;
    width: 33%;
    justify-content: space-around;
    margin-left: 1rem;
}

dialog {
    width: 80%;
    position:fixed;
    margin:auto;
    top: -20%;
    background-color: #696969;
    color: #efefef;
    border-radius: 0.5rem;
    border-width: 0px;
    z-index: 1000;
}

dialog::backdrop {
    background-color: #000000;
    opacity: 20%;
}

.focused {
    display: flex;
    flex-direction: column;
}

button {
    background-color: #a0a0a0;
}
</style>