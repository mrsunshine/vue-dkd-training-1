<template>
  <users @user-change="onUserChange" />
  <h1 v-if="user">Aktueller User {{ user.name }}</h1>
  <posts :userId="user.id" />
  <!--
  <h1>{{ userMsg }}</h1>
  <HelloWorld msg="Guten Morgen!" :showList="true" />
  <HelloWorld
    msg="Guten Abend!"
    :showList="false"
    @super-button-click="onSuperButtonClick"
  />
  -->
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import posts from './components/Posts.vue';
import users from './components/Users.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    posts,
    users,
  },
  data() {
    return {
      userMsg: '',
      user: {
        id: null,
      },
    };
  },

  methods: {
    onUserChange(user) {
      this.user = user;
    },

    onSuperButtonClick(counter, userObj, userName, testString) {
      console.log('onSuperButtonClick', counter, userObj, userName, testString);

      // this.userMsg = userName + ' ' + counter + ' ' + testString;
      this.userMsg = `${userName} ${counter} ${testString}`;
    },
  },
};
</script>

<style>
#app {
}
</style>
