<template>
  <div id="app">
    <header>
      <h1>Vue+AWS SAM Example</h1>
      <p>Featuring CallOfDuty API</p>
      <p>{{ message }}</p>
    </header>
    
    <Leaderboard :gamers=gamers />
  </div>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator'
import fetch from 'cross-fetch'
import Leaderboard from './components/Leaderboard.vue'

@Component({
  components: {
    Leaderboard,
  }
})
export default class App extends Vue {
  message = 'Loading...';
  gamers = {}; // Payload with COD Leaderboad gamers data 

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
      console.log("COD endopoint is " + message);
      
      // console.log(data);
      const { platform, leaderboardType, entries } = data.codApiResponse;

      this.gamers =  {      
        platform : platform,
        type: leaderboardType,
        leaders: entries
      }
    }
  }

}
</script>