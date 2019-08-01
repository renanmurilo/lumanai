<template>
  <section>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <div v-for="(post, index) in posts" :key="index">
            <router-link :to="{name: 'post', params: {id: post.id}}">
              <div>
                <h2>{{post.title}}</h2>
                <p>{{post.body}}</p>
              </div>
            </router-link>
          </div>
          <PostsPaginar :postsTotal="postsTotal" :postsPorPagina="postsPorPagina" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import PostsPaginar from "@/components/PostsPaginar.vue";
import { api } from "@/service.js";
import { serialize } from "@/helpers.js";

export default {
  name: "posts",
  components: {
    PostsPaginar
  },
  data() {
    return {
      posts: null,
      postsPorPagina: 10,
      postsTotal: 0
    };
  },
  computed: {
    url() {
      const query = serialize(this.$route.query);
      return `/?_limit=${this.postsPorPagina}${query}`;
    }
  },
  methods: {
    getPosts() {
      this.posts = null;
      api.get(this.url).then(response => {
        this.postsTotal = Number(response.headers["x-total-count"]);
        this.posts = response.data;
      });
    }
  },
  watch: {
    url() {
      this.getPosts();
    }
  },
  created() {
    this.getPosts();
  }
};
</script>

<style>
</style>
