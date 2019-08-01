<template>
  <section>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <div v-if="posts.id">
            <h2>{{posts.title}}</h2>
            <p>{{posts.body}}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { api } from "@/service.js";

export default {
  name: "PostsItem",
  props: ["id"],
  data() {
    return {
      posts: null
    };
  },
  methods: {
    getPostsItem() {
      api.get(`/${this.id}`).then(response => {
        this.posts = response.data;
      });
    }
  },
  created() {
    this.getPostsItem();
  }
};
</script>

<style>
</style>
