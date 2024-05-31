<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import DifficultyLable from '@/components/DifficultyLable.vue';
const dif = ref(1);
const tits = defineModel('tits', { type: String });
const bod = defineModel('bod', { type: String });
let stars = [];
stars = calc_stars();
const router = useRouter()

function calc_stars() {
    let stars = [];
    for(let i = 0; i < 10; i++){
        if(dif.value <= i){
            stars.push(ref("☆"));
        } else {
            stars.push(ref("★"));
        }
    }
    return stars;
}

function dif_update(value) {
    dif.value = value;
    dif_show(value+1);
}

function dif_show(value) {
    for(let i = 0; i < 10; i++){
        if(value <= i){
            stars[i].value ="☆";
        } else {
            stars[i].value = "★";
        }
    }
}

async function submit_post (){
    let new_post = await fetch(import.meta.env.VITE_BACKEND_URL+"newpost/", { 
      method: "POST",
      mode: "cors",
      headers: {'content-type':"application/json"},
      credentials: "omit",
      body: JSON.stringify({
          title: tits.value,
          body: bod.value,
          challange: dif.value,
      })
    });
    console.log(new_post)
    router.push("/forum")
}
</script>

<template>
<main>
    <h2>Submit a Challange</h2>
    <div @mouseleave="dif_update(dif)">
        <p>Difficulty: </p>
        <p style="cursor: pointer;" v-for="(star, index) in stars" @mouseover="dif_show(index+1)" @click="dif_update(index)" >{{ star.value }}</p>
    </div>
    <DifficultyLable :difficulty="dif" class="cere"/>
    <input v-model="tits" class="text" autocomplete="off" placeholder="Title of the Challange. Preferably with Challange type included">
    <textarea v-model="bod"class="text" autocomplete="off" placeholder="Description of the Challange."></textarea>
    <button @click="submit_post(); router.push()">Submit</button>
   
</main>

</template>

<style scoped>
div {
    display:flex
}
p {
    font-size: large;
    padding-right: 0.25rem;
}
.text {
    margin: 0.25rem 0rem;
}

main{
    width: auto;
    display: flex;
    flex-direction: column;
}

button{
    width: fit-content;
    background-color: var(--vt-c-black-soft);
    color: var(--color-text);
    border:2px;
    transition: background-color .15s ease-in-out;
}

button:hover{
    background-color: hsla(160, 100%, 37%, 0.4);
}

button:active{
    background-color: hsla(160, 100%, 37%, 0.2);
}


</style>