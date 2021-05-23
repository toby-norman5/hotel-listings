<template>
  <div>
    <div class="flex flex-col border border-gray-300 shadow-md">
      <img :src="`https://hi-cdn.t-rp.co.uk/images/hotels/${hotel.imageId}/0?width=300&height=150&crop=false`"
           :alt="`${hotel.title}`" loading="lazy" class="w-full" style="height: 150px;">
      <div class="flex flex-col text-left p-3">
        <h2 class="text-lg font-bold text-blue-600 mb-1">{{ hotel.title }}</h2>
        <div class="flex">
          <div v-for="n in hotel.starRating" :key="n">
            <span class="material-icons md-18 text-yellow-400">star</span>
          </div>
        </div>
        <div class="text-sm mb-4">{{ hotel.description }}</div>
        <div class="flex items-center">
          <div class="px-3 py-1 bg-blue-500 text-white font-bold">{{ hotel.userRating }}</div>
          <span class="material-icons-outlined md-24 text-blue-400 px-2">{{ userRatingIcon }}</span>
          <div class="flex items-center text-blue-400 text-sm">
            (based on {{ reviewCount }} reviews)
          </div>
        </div>
        <hr class="my-5">
        <div class="text-sm italic mb-3">Price includes:</div>
        <div class="flex items-center mb-1">
          <span class="material-icons md-18 text-yellow-600 mr-3">restaurant</span>
          <div class="text-sm">{{ hotel.itemsIncludedInPrice.meals ? 'Breakfast, Dinner' : 'Room only' }}</div>
        </div>
        <div class="flex items-center">
          <span class="material-icons md-18 text-yellow-600 mr-3">paid</span>
          <div class="text-sm">
            {{ hotel.itemsIncludedInPrice.localTaxes ? 'Local charges payable at hotel' : 'No extra charges' }}
          </div>
        </div>
      </div>
      <div class="flex justify-between bg-gray-100 border-t border-dashed border-gray-300 p-3 mt-1">
        <div class="flex flex-col text-left">
          <div class="text-xs">Total price from</div>
          <div class="text-2xl text-yellow-600 font-bold">£{{ hotel.pricePerPersonGBP * travellerCount }}</div>
          <div class="text-xs">(Per Person <span class="font-bold">£{{ hotel.pricePerPersonGBP }}</span>)</div>
        </div>
        <div class="flex items-center">
          <button class="bg-yellow-600 text-white font-bold px-6 py-3">View More</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HotelCard",
  props: ['hotel', 'travellerCount'],
  data() {
    return {
      reviewCount: Math.round(Math.random() * 100)
    }
  },
  computed: {
    userRatingIcon() {
      if (this.hotel.userRating < 4) {
        return 'sentiment_dissatisfied'
      } else if (this.hotel.userRating < 7) {
        return 'sentiment_neutral'
      }

      return 'sentiment_very_satisfied'
    }
  }
}
</script>

<style scoped>
.material-icons.md-18 {
  font-size: 18px;
}
</style>