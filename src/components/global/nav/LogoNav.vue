<template>
  <div>
    <!-- <router-link :to="{ name: 'home' }"
      ><img :class="props.classes" src="@/assets/images/logo.png"
    /></router-link> -->
    <img
      :class="props.classes"
      src="@/assets/images/logo.png"
      @click="$router.push({ name: 'home' })"
      style="cursor: pointer"
    />
  </div>
</template>
<script setup>
import { defineProps } from "vue";
const props = defineProps({
  classes: {
    type: String,
  },
});
</script>
