<template>
  <h1>{{ userMsg }}</h1>
  <HelloWorld msg="Guten Morgen!" :showList="true" />
  <HelloWorld
    msg="Guten Abend!"
    :showList="false"
    @super-button-click="onSuperButtonClick"
  />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      userMsg: '',
    };
  },

  methods: {
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
