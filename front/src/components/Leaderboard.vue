<template>
  <section>
    <div>gamers.platform</div>
    <div>gamers.type</div>
    <div :key="gamer.id" v-for="gamer in gamers">
      <Gamer gamer="gamer" />
    </div>
  </section>
</template>

<script>
  import Gamer from './Gamer';
  export default {
    name: 'Leaderboard',
    components: { Gamer },
    props: gamers,
    // data() {
    //   return {
    //     codApiContent:
    //   }
    // }
  }
</script>
