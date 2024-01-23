<!-- <script>
import { createApp, ref } from 'vue'

createApp({
  setup() {
    return {
      count: ref(0)
    }
  }
}).mount('#app')
</script>

<template>
    <div id="app">
        <button @click="count++">
            Count is: {{ count }}
        </button>
    </div>
</template> -->

<script setup>
import { ref } from 'vue'
const count = ref(0)
const props = defineProps({toggle:{type:Number}});
const emitter = defineEmits(["passToggle"]);

function handleClick() {
    count.value = 0;
    emitter("passToggle");
}
</script>

<script>                                 
export default {
    emits: ["passToggle"],
    methods:{
        passToggle()
        {
            thisswit();
            this.$emit('toggleSwitch', props.toggle);
        }
    }
}
</script>

<template>
  <button @click="count++">Count is: {{ count }}</button>
  <button @click="handleClick">Reset value</button>
</template>

<style scoped>
button {
  font-weight: bold;
  background-color: black;
  color:gray;
  border:0;
  padding:1;
}
</style>