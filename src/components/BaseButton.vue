<template>
 <div>
    <button
      :class="style"
    > {{ textbutton }}</button>
 </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

defineProps({
   style:{
    type: String,
    default:'mb-4 py-2 px-4 mx-4 rounded-md  rounded-md bg-blue-500 hover:bg-blue-700 transition delay-150 duration-300 ease-in-out',
   },
   textbutton:{
    type: String
   }
})
</script>