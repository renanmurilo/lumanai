<template>
  <div class="home">
    <Posts />
  </div>
</template>

<script>
import Posts from "@/components/Posts.vue";

export default {
  name: "home",
  components: {
    Posts
  },
  created() {
    document.title = "Lumanai";
  }
};
</script>
