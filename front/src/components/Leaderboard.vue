<template>
  <section>
    <div><strong>Platform: </strong> {{ gamers.platform }}</div>
    <div><strong>Type: </strong> {{ gamers.type }}</div>
    
      <Gamer :key="gamer.rank" v-for="gamer in gamers.leaders" :gamer="gamer" />
    
  </section>
</template>

<script>
  import Gamer from './Gamer';
  export default {
    name: 'Leaderboard',
    components: { Gamer },
    props: ['gamers'],
  }
</script>
