<script setup>
import { defineProps } from 'vue';
import TheWelcome from '../components/TheWelcome.vue'
const props = defineProps({disabled:{type:Number, default:1}})
</script>

<template>
  <main>
    <TheWelcome v-bind:show="props.disabled" />
  </main>
</template>
