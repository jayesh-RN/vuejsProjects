<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Sportz Interactive</a>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <select
              v-model="selectedTeam"
              @change="filterPlayers"
              class="form-select"
            >
              <option value="ALL">ALL</option>
              <option value="IND">IND</option>
              <option value="PAK">PAK</option>
              <option value="AUS">AUS</option>
              <option value="ENG">ENG</option>
            </select>
          </ul>
          <form class="d-flex" role="search">
            <input
              class="form-control me-2"
              type="search"
              placeholder="Search"
              v-model="searchQuery"
              @input="filterPlayers"
            />
            <button
              class="btn btn-outline-success"
              type="button"
              @click="searchPlayers"
            >
              Search
            </button>
          </form>
        </div>
      </div>
    </nav>

    <div class="container text-center">
      <PlayerList :players="filteredPlayers" role="2" title="Batsmen" />
      <PlayerList :players="filteredPlayers" role="4" title="Bowlers" />
      <PlayerList :players="filteredPlayers" role="3" title="All-rounders" />
    </div>
  </div>
</template>

<script>
import PlayerList from "./components/PlayerList.vue";
import playersData from "./data/players.json";

export default {
  name: "App",
  components: {
    PlayerList,
  },
  data() {
    return {
      originalPlayers: playersData.originalPlayers,
      filteredPlayers: [],
      selectedTeam: "ALL",
      searchQuery: "",
    };
  },
  mounted() {
    this.filterPlayers();
  },
  methods: {
    filterPlayers() {
      let filtered = this.originalPlayers;

      if (this.selectedTeam !== "ALL") {
        filtered = filtered.filter(
          (player) => player.team_name === this.selectedTeam
        );
      }

      const query = this.searchQuery.toLowerCase();
      if (query) {
        filtered = filtered.filter(
          (player) =>
            player.name.toLowerCase().includes(query) ||
            player.team_name.toLowerCase().includes(query)
        );
      }

      this.filteredPlayers = filtered;
    },
    searchPlayers() {
      this.filterPlayers();
    },
  },
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
}

#app {
  margin: 20px;
}

.navbar {
  border-bottom: 1px solid #ddd;
  background-color: #ffffff;
}

.navbar-brand {
  font-size: 1.5rem;
  font-weight: bold;
  color: #007bff;
}

.navbar-nav .form-select {
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
}

.form-control {
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
}

.form-control:focus {
  border-color: #80bdff;
  box-shadow: 0 0 0 0.2rem rgba(38, 143, 255, 0.25);
}

.btn-outline-success {
  color: #28a745;
  border-color: #28a745;
}

.btn-outline-success:hover {
  background-color: #28a745;
  color: #ffffff;
}

.container {
  background-color: #ffffff;
  border-radius: 0.25rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-top: 20px;
}

h1 {
  color: #343a40;
  margin-bottom: 20px;
}

@media (max-width: 768px) {
  .navbar-nav .form-select {
    margin-bottom: 10px;
  }

  .form-control {
    width: 100%;
    margin-bottom: 10px;
  }
}
</style>
