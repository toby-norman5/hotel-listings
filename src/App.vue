<template>
  <NavBar></NavBar>
  <div class="flex" style="height: calc(100vh - 70px)">
    <SideMenu :travellerCount="travellerCount"
              @updateSearchResults="searchHotels"
              @updateTravellerCount="changeInCount => travellerCount += changeInCount"></SideMenu>
    <div class="flex flex-col w-full px-2 py-4 sm:p-4 md:p-10 overflow-y-scroll">
      <h2 class="font-bold mb-6">Showing {{ filteredHotels.length }} of {{ hotels.length }} results</h2>
      <div id="hotel-grid">
        <div v-for="hotel in filteredHotels" :key="hotel.id">
          <HotelCard :hotel="hotel" :travellerCount="travellerCount"></HotelCard>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import NavBar from './components/NavBar.vue';
import SideMenu from './components/SideMenu.vue';
import HotelCard from './components/HotelCard.vue';

export default {
  name: 'App',
  components: {
    NavBar,
    SideMenu,
    HotelCard
  },
  data() {
    return {
      hotels: [],
      filteredHotels: [],
      travellerCount: 1
    }
  },
  mounted() {
    this.fetchHotels();
  },
  methods: {
    async fetchHotels() {
      let response = await axios.get('http://localhost:3000/hotels');
      this.hotels = response.data;
      this.filteredHotels = response.data;
    },
    searchHotels(searchText) {
      this.filteredHotels = this.hotels.filter(hotel => {
        return hotel.title.toLowerCase().includes(searchText.toLowerCase());
      })
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#hotel-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-auto-rows: minmax(auto, auto);
  grid-gap: 20px;
}
</style>
