<template>
  <div id="app">
    <TheHeader />
    <transition mode="out-in">
      <router-view />
    </transition>
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader.vue";

export default {
  components: {
    TheHeader
  }
};
</script>
<style>
</style>
