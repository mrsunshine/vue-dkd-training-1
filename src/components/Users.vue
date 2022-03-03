<template>
  <h3>Users</h3>

  <button v-for="(user, index) in users" @click="onClick(user)">
    {{ user.name }}
  </button>
</template>
<script>
export default {
  name: 'Users',

  data() {
    return {
      users: null,
    };
  },
  created() {
    fetch(`https://jsonplaceholder.typicode.com/users`)
      .then((response) => response.json())
      .then((json) => (this.users = json));
  },
  methods: {
    onClick(user) {
      console.log(user);
      this.$emit('user-change', user);
    },
  },
};
</script>
<style></style>
