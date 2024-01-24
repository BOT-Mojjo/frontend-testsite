<script setup>
import { ref } from 'vue';
const dif = ref(0);
let stars = [];
stars = calc_stars();


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
    dif_show(value);
}

function dif_show(value) {
    for(let i = 0; i < 10; i++){
        if(value+1 <= i){
            stars[i].value ="☆";
        } else {
            stars[i].value = "★";
        }
    }
}
</script>

<template>
<main>
    <h1> lmao </h1>
    <div @mouseleave="dif_update(dif)">
        <p v-for="(star, index) in stars" @mouseover="dif_show(index)" @click="dif_update(index)" >{{ star.value }}</p>
    </div>
</main>

</template>

<style>

</style>