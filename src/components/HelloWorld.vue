<template>
  <div class="hello">
    <h1>{{ msg }} {{ counter }}</h1>
    <h3>Hat {{ fullName }} lustige Hobbys? {{ hasFunHobbys }}</h3>
    <p>showList: {{ showList }}</p>

    <button :disabled="showList" :class="cssClass" @click="onButtonClick">
      Counter ({{ counter }})
    </button>

    <button
      :disabled="showList"
      v-bind:class="showList ? 'super-button' : 'dkd-button'"
    >
      test dkd
    </button>
    <button
      :disabled="showList"
      :class="getCssClass() + ' test2 ' + cssClass"
      :class="cssClass"
    >
      test dkd
    </button>
    <ul>
      <li v-for="(hobby, index) in user.hobbys.fun" :key="index">
        <template v-if="index"> {{ index + 1 }}: {{ hobby }} </template>
      </li>
    </ul>

    <ul>
      <li v-for="(value, key) in user" :key="key">
        <template v-if="typeof value === 'object'">
          <ul>
            <li v-for="(valueChild, keyChild) in value" :key="keyChild">
              {{ valueChild }}
            </li>
          </ul>
        </template>
        {{ value }}
      </li>
    </ul>

    <ul v-if="showList">
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel"
          target="_blank"
          rel="noopener"
          >babel</a
        >
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint"
          target="_blank"
          rel="noopener"
          >eslint</a
        >
      </li>
    </ul>
    <pre v-else-if="user.name === 'Niels'">
      {{ user }}
    </pre>
    <p v-else>Worst case</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    showList: {
      type: Boolean,
      default: () => true,
    },
  },
  created() {
    console.log('created', this.user);
  },
  mounted() {
    console.log('mounted Hurra hurra das DOM ist da ;-)');
  },
  data() {
    return {
      counter: 1,
      cssClass: 'super-button',
      user: {
        name: 'Nils',
        nachname: 'Dehl',
        hobbys: {
          fun: ['vue', 'Humor', 'Minigolf'],
          sport: 'crossfit',
        },
      },
    };
  },
  watch: {
    counter(newValue, oldValue) {
      console.log('counter', newValue, oldValue);
    },
    user: {
      deep: true,
      handler(newValue, oldValue) {
        console.log('user', newValue, oldValue);
      },
    },
  },
  computed: {
    fullName() {
      return this.user.name + ' ' + this.user.nachname;
    },
    hasFunHobbys() {
      return this.user.hobbys.fun.length ? 'JA hat er' : ' Nein :-(';
    },
  },
  methods: {
    onButtonClick() {
      this.counter++;
      this.user.hobbys.fun.push('vue');

      this.$emit(
        'super-button-click',
        this.counter,
        this.user,
        this.user.name,
        'test'
      );
    },
    getCssClass() {
      return this.showList ? 'super-button' : 'dkd-button';
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}

.super-button {
  background-color: red;
}

.dkd-button {
  background-color: green;
}
</style>
