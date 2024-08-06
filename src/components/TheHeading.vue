<template>
<header>
    <h1 :class='style'
    >Weather</h1>
  </header>
</template>

<script setup lang="ts">
import {defineProps} from 'vue';

defineProps({
  style:{
    type:String,
    default:'mt-4 text-center mb-6 text-2xl font-bold',
  },
}
)
</script>