<template>
  <div>
    <h3>ID: {{ gamer.rank }}</h3>
    <h4>{{ gamer.username }}</h4>
  
    <p><span>Kills: </span>{{ gamer.values.kills }}</p>
    <p><span>Level: </span>{{ gamer.values.level }}</p>
    <p><span>Accuracy: </span>{{ gamer.values.accuracy }}</p>
    <p><span>Score: </span>{{ gamer.values.score }}</p>
    <p><span>Assists: </span>{{ gamer.values.assists }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Gamer',
    props: ['gamer'],
  }
</script>

<style scoped>
  h3 {
    font-weight: bold;
  }
</style>
