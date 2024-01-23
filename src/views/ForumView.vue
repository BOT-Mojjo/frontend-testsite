<script setup>
import listing from '@/components/listing.vue';

</script>

<template>
    <div>
        <listing Title="Test 1" :Discription=disc Difficulty="1"></listing>
        <listing Title="Test 2" :Discription=disc Difficulty="2"></listing>
        <listing Title="Test 3" :Discription=disc Difficulty="3"></listing>
        <listing Title="Test 4" :Discription=disc Difficulty="4"></listing>
        <listing Title="Test 5" :Discription=disc Difficulty="5"></listing>
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