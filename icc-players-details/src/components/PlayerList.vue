<template>
    <div class="row player-row">
      <h1>{{ title }}</h1>
      <div class="col" v-for="player in filteredPlayers" :key="player.name">
        <PlayerCard :player="player" />
      </div>
    </div>
  </template>
  
  <script>
  import PlayerCard from './PlayerCard.vue';
  
  export default {
    name: 'PlayerList',
    components: {
      PlayerCard
    },
    props: {
      players: Array,
      role: String,
      title: String
    },
    computed: {
      filteredPlayers() {
        return this.players.filter(player => player.role === parseInt(this.role));
      }
    }
  };
  </script>