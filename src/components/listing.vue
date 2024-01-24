<script setup>
import { computed } from 'vue';
const props = defineProps(["Title", "Discription", "Difficulty"]);
const star_str = computed(calc_stars);
const dif_word = ["Minor", "Lesser", "Standard", "Major", "Greater"];

let decider = Math.floor((props.Difficulty)/2-0.5);
if(decider < 0) decider = 0;


function calc_stars() {
    let stars = [];
    for(let i = 0; i < 10; i++){
        if(props.Difficulty <= i){
            stars.push("☆");
        } else {
            stars.push("★");
        }
    }
    return stars;
}


</script>
<!-- ☆ ★ -->
<template>
    <article @click="$emit('focus')">
        <main>
            <h3>{{ props.Title }}</h3>
            <p>{{ props.Discription }}</p>
        </main>
        <aside>
            <h4>{{ dif_word[decider] }} Infestation</h4>
            <div class="stars">    
                <b v-for="star in star_str">
                    {{ star }}
                </b>
            </div>
        </aside>
    </article>
</template>

<style>

p{
    overflow-wrap: break-word;
}

.stars{
    display:grid;
    grid-template-rows: repeat(5, 1.5rem);
    grid-template-columns: repeat(2, 1.5rem);
}
h4 {
    width:4.5rem;
}
main{
    width:25rem;
}
article {
    display: flex;
    flex-flow: row nowrap;
    justify-content:space-between;
    width:32rem;
    padding:0.5rem;
    padding-top: 0.25rem;
    padding-bottom: 0.25rem;
    transition: background-color .15s ease-in-out;
    margin:.5rem;
    border-radius: 0.25rem;
    cursor: pointer;
}


article:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
}

b {
    justify-self: center;
    grid-column: auto;
    grid-row:auto;
}

</style>