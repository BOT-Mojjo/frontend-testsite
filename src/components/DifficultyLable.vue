<script setup>
import { ref, computed, onRenderTriggered } from 'vue';
const props = defineProps(['difficulty']);
const dif_word = ["Minor", "Lesser", "Standard", "Major", "Greater"];

let word = computed(() => {
    let decider = Math.floor((props.difficulty-1)/2);
    decider = decider > 0 ? decider : 0;
    return dif_word[decider];
});
</script>

<template>
<h4>{{ word }} Challange</h4>
</template>
<style scoped>
h4{
    width:4.5rem;
}
</style>
