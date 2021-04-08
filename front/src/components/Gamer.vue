<template>
  <div>
    <h3> {{ gamer.id }}</h3>
    <h4>{{ gamer.username }}</h4>
  
    <p>{{ gamer.kills }}</p>
    <p>{{ gamer.level }}</p>
    <p>{{ gamer.accuracy }}</p>
    <p>{{ gamer.score }}</p>
    <p>{{ gamer.assists }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Gamer',
    props: gamer,
  }
</script>

<style scoped>
  h3 {
    font-weight: bold;
  }
</style>
