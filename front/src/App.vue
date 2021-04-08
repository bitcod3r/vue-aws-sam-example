<template>
  <div id="app">
    <header>
      <h1>Vue+AWS SAM Example</h1>
      <p>Featuring CallOfDuty API</p>
      <p>{{ message }}</p>
    </header>
    
    <Leaderboard :gamers="gamers" />
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
  codApiContent = 'Loading...';
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
      console.log("COD endopoint is " + this.message);
      const { message, data } = await resCodApi.json();
      this.gamers = this.getGamers(data);
    } else {
      // Set gamers without values.
    }
  }
  
  getGamers(payload) {
    let gamers : { 
                    platform: String,
                    type: String,
                    leaders: Array<{
                      id: Number,
                      username: String,
                      kills: Number,
                      level: Number,
                      accuracy: Number,
                      score: Number,
                      assists: Number,
                    }>
                 }

    gamers = { 
              platform: "battle",
              type: "core",
              leaders: [
                {
                  id: 1,
                  username: "guizao23#6674996",
                  kills: 1242,
                  level: 80,
                  accuracy: 111,
                  score: 123,
                  assists: 6342
                },
                {
                  id: 2,
                  username: "guizao23#6674996",
                  kills: 1242,
                  level: 80,
                  accuracy: 111,
                  score: 123,
                  assists: 6342
                },
                {
                  id: 3,
                  username: "guizao23#6674996",
                  kills: 1242,
                  level: 80,
                  accuracy: 111,
                  score: 123,
                  assists: 6342
                },
                {
                  id: 4,
                  username: "guizao23#6674996",
                  kills: 1242,
                  level: 80,
                  accuracy: 111,
                  score: 123,
                  assists: 6342
                },
              ]
            }
      

/*
  gamers.platform = codApiResponse.platform
  gamers.type = codApiResponse.leaderboardType

  let entries = payload.entries

  for(let key in entries) {
    gamers.leaders.push({
      id= key.rank,
      username= key.username,
      kills= key.kills,
      level= key.level,
      accuracy= key.accuracy,
      score= key.score,
      assists= key.assists
    })
  }


*/

    return gamers;
  }

}
</script>