<template>
  <div id="app">
    <h1>Welcome to the challenge app</h1>
    <p>{{ message }}</p>
  </div>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator'

@Component
export default class App extends Vue {
  message = 'Loading...'

  async mounted() {
    const res = await fetch('http://localhost:3000/hello');
    if (res.ok) {
      const { message } = await res.json();
      this.message = message;
    }
  }
}
</script>