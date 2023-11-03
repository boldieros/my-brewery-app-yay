<template>
  <div class="app-background">
    <div class="app-content">
      <h1 class="app-title">My Brewery App</h1>
      <input v-model="searchTerm" @input="searchBreweries" placeholder="Search for breweries">
      <ul>
        <li v-for="brewery in breweries" :key="brewery.id">
          {{ brewery.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      breweries: [],
      searchTerm: ''
    };
  },
  mounted() {
    this.fetchBreweries();
  },
  methods: {
    fetchBreweries() {
      const apiUrl = 'https://api.openbrewerydb.org/breweries';
      axios.get(apiUrl).then(response => {
        this.breweries = response.data;
      });
    },
    searchBreweries() {
      const apiUrl = 'https://api.openbrewerydb.org/breweries';
      const searchQuery = this.searchTerm;

      axios.get(apiUrl, { params: { name: searchQuery } }).then(response => {
        this.breweries = response.data;
      });
    }
  }
};
</script>

<style scoped>
.app-background {
  background-image: url('./spacedust.jpg'); /* Replace with the correct path to your image */
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-color: #000; /* Fallback background color */
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.app-content {
  text-align: center;
  color: #fff;
}

.app-title {
  font-size: 36px;
  margin-bottom: 20px;
}
</style>
