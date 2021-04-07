<template>
  <div id="app">
    <h1>Welcome to the challenge app</h1>
    <p>{{ message }}</p>
    <div>
      {{ codApiContent }}
    </div>
  </div>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator'
import fetch from 'cross-fetch';

@Component
export default class App extends Vue {
  message = 'Loading...';
  codApiContent = 'Loading...';

  async mounted(): Promise<void> {
    
    const res = await fetch('http://localhost:3000/hello');
    if (res.ok) {
      const { message } = await res.json();
      this.message = message;
    }

    // Reaching out second Lambda
    const resCodApi = await fetch('http://localhost:3000/cod');
    if (resCodApi.ok) {
      const { message, data } = await resCodApi.json();
      this.codApiContent = JSON.stringify(data);
      console.log("COD endopoint is " + message);
    }
  }

}
</script>