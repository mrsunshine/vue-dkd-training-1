<template>
  <h3>Alle User Posts</h3>
  <ul v-if="posts && !loading">
    <li v-for="(post, index) in posts">
      <h3>{{ post.title }}</h3>
      <p>{{ post.body }}</p>
    </li>
  </ul>
  <p v-else-if="loading">Daten werden geladen...</p>

  <p v-else-if="!posts">Keine Posts vorhanden</p>

  <p>Debug Infos: UserID ={{ userId }}</p>
</template>
<script>
export default {
  name: 'Posts',
  props: {
    userId: Number,
  },
  data() {
    return {
      posts: null,
      loading: false,
    };
  },
  watch: {
    userId() {
      this.loadData();
    },
  },
  created() {
    this.loadData();
  },
  methods: {
    loadData() {
      if (this.userId) {
        this.loading = true;
        fetch(`https://jsonplaceholder.typicode.com/users/${this.userId}/posts`)
          .then((response) => response.json())
          .then((json) => {
            this.posts = json;
            this.loading = false;
          });
      }
    },
  },
};
</script>
<style></style>
