<template>
    <div class="card">
      <img :src="player.image" class="card-img-top" alt="Player Image">
      <div class="card-body">
        <h5 class="card-title">{{ player.name }}</h5>
        <p class="card-text">Matches: {{ player.matches }}</p>
        <p class="card-text">Runs: {{ player.runs }}</p>
        <p class="card-text">50s/100s: {{ player['50s'] }}/{{ player['100s'] }}</p>
        <p class="card-text">Highest Score: {{ player.highest_score }}</p>
        <p class="card-text">Team Name: {{ player.team_name }}</p>
        <p class="card-text">Best Bowling Figures: {{ player.best_bowling_figures }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PlayerCard',
    props: {
      player: Object
    }
  };
  </script>
  