<template>
  <ul v-if="postsTotal > 1">
    <li v-for="pagina in paginas" :key="pagina">
      <router-link :to="{query: query(pagina)}">{{pagina}}</router-link>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    postsPorPagina: {
      type: Number,
      default: 1
    },
    postsTotal: {
      type: Number,
      default: 1
    }
  },
  methods: {
    query(pagina) {
      return {
        ...this.$route.query,
        _page: pagina
      };
    }
  },
  computed: {
    paginas() {
      const current = Number(this.$route.query._page);
      const range = 10;
      const offset = Math.ceil(range / 2);
      const total = this.postsTotal;
      const pagesArray = [];

      for (let i = 1; i <= total; i++) {
        pagesArray.push(i);
      }

      pagesArray.splice(0, current - offset);
      pagesArray.splice(range, total);

      return pagesArray;
    },
    paginasTotal() {
      const total = this.postsTotal / this.postsPorPagina;
      return total !== Infinity ? Math.ceil(total) : 0;
    }
  }
};
</script>

<style scoped>
ul {
  display: flex;
  justify-content: flex-end;
  list-style: none;
}

li {
  margin: 0.1rem;
}

li a {
  padding: 2px 8px;
  border-radius: 2px;
}

a {
  color: #000000;
  text-decoration: none;
}

li a.router-link-exact-active,
li a:hover {
  background: #000000;
  color: #fff;
}
</style>
