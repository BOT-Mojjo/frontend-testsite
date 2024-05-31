<script setup>
import { computed } from 'vue';
import diffLable from './DifficultyLable.vue';
const props = defineProps(["title", "discription", "difficulty"]);
const star_str = computed(calc_stars);



function calc_stars() {
    let stars = [];
    for(let i = 0; i < 10; i++){
        if(props.difficulty <= i){
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
            <h3>{{ props.title }}</h3>
            <p>{{ props.discription }}</p>
        </main>
        <aside>
            <diffLable :difficulty="props.difficulty"/>    
            <div class="stars">
                <b v-for="star in star_str">
                    {{ star }}
                </b>
            </div>
        </aside>
    </article>
</template>

<style scoped>

p{
    overflow-wrap: break-word;
}

.stars{
    display:grid;
    grid-template-rows: repeat(5, 1.5rem);
    grid-template-columns: repeat(2, 1.5rem);
}
main{
    width:80%;
}
article {
    display: flex;
    flex-flow: row nowrap;
    justify-content:space-between;
    width: 100%;
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