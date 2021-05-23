<template>
  <div class="hidden lg:flex flex-col items-start border-r-2 border-yellow-600 py-6 px-5" style="min-width: 300px;">
    <div class="w-full mb-5">
      <h3 class="rounded-t bg-yellow-600 font-bold text-white">Search</h3>
      <div class="flex border border-gray-200 p-2">
        <input type="text" placeholder="Search for hotels..." v-model="searchText" @keyup="updateSearchResults"
               class="w-full">
      </div>
    </div>

    <div class="w-full mb-5">
      <h3 class="rounded-t bg-yellow-600 font-bold text-white">Travellers</h3>
      <div class="flex items-center justify-around border border-gray-200 p-2">
        <button @click="decreaseTravellerCount" class="bg-yellow-600 text-white font-bold rounded px-2">-</button>
        <span>{{ travellerCount }}</span>
        <button @click="increaseTravellerCount" class="bg-yellow-600 text-white font-bold rounded px-2">+</button>
      </div>
    </div>

    <div class="w-full mb-5">
      <h3 class="rounded-t bg-yellow-600 font-bold text-white">Sort By</h3>
      <div class="border border-gray-200 text-sm p-2">
        <div class="flex items-center">
          <input type="radio" name="sort" class="mr-2">
          <div>Star Rating</div>
        </div>
        <div class="flex items-center">
          <input type="radio" name="sort" class="mr-2">
          <div>User Rating</div>
        </div>
        <div class="flex items-center">
          <input type="radio" name="sort" class="mr-2">
          <div>Total Price</div>
        </div>
      </div>
    </div>

    <div class="w-full">
      <h3 class="rounded-t bg-yellow-600 font-bold text-white">Filter</h3>
      <div class="border border-gray-200 text-sm p-2">
        <div class="flex items-center">
          <input type="checkbox" class="mr-2">
          <div v-for="n in 5" :key="n">
            <span class="material-icons md-18 text-yellow-400">star</span>
          </div>
        </div>
        <div class="flex items-center">
          <input type="checkbox" class="mr-2">
          <div v-for="n in 4" :key="n">
            <span class="material-icons md-18 text-yellow-400">star</span>
          </div>
        </div>
        <div class="flex items-center">
          <input type="checkbox" class="mr-2">
          <div v-for="n in 3" :key="n">
            <span class="material-icons md-18 text-yellow-400">star</span>
          </div>
        </div>
        <div class="flex items-center">
          <input type="checkbox" class="mr-2">
          <div v-for="n in 2" :key="n">
            <span class="material-icons md-18 text-yellow-400">star</span>
          </div>
        </div>
        <div class="flex items-center">
          <input type="checkbox" class="mr-2">
          <div v-for="n in 1" :key="n">
            <span class="material-icons md-18 text-yellow-400">star</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SideMenu",
  props: ['travellerCount'],
  emits: ['updateSearchResults', 'updateTravellerCount'],
  data() {
    return {
      searchText: ''
    }
  },
  methods: {
    updateSearchResults() {
      this.$emit('updateSearchResults', this.searchText);
    },
    increaseTravellerCount() {
      this.$emit('updateTravellerCount', 1);
    },
    decreaseTravellerCount() {
      if (this.travellerCount > 0) {
        this.$emit('updateTravellerCount', -1);
      }
    }
  }
}
</script>

<style scoped>

</style>