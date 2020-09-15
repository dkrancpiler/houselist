<template>
  <div>
    <h1>List of available real estate objects for rent or sale</h1>
    <template v-for="(house, index) in houses">
      <div :key="house.id">{{house.seo_title}}
        <n-link :to="'/houses/' + house.id">
          <img v-if="images[index]" alt ="Image is unavailable" class ="image" height = "200" width ="200" v-bind:src="`${$config.apiUrl}/api/media/` + images[index][0].id">
          <span v-else>Image of this house is unavailable</span>
          <p>{{house.seo_desc}}</p>
          <p>The address of this real estate object is: {{house.address}}</p>
          <p v-if="house.price">Price is: {{house.price}}€</p>
          <p v-else>The price of this house is unavailable!</p>
        </n-link>
      </div>
    </template>
<!--    <pagination>-->

<!--    </pagination>-->
<!--    <ul>-->
<!--      <li v-for="house of houses" :key="house.id">-->
<!--        <span @click="pushToSingle(house)">{{house.title}}</span>-->
<!--      </li>-->
<!--    </ul>-->
<!--    <span>{{pagination}}</span>-->
  </div>
</template>

<script>
import axios from "axios"
import Pagination from "@/components/pagination";
require('dotenv').config({path: 'C:/Users/TogoInPogo/houselist/.env'})
export default {
  components: {Pagination},
  data(){
    return{
      houses: [],
      pagination: {},
      media: [],
      images: []
    }
  },

  async mounted () {
    try {
      let { data } = await axios.get (`${this.$config.appUrl}/api/home`)
      this.houses=data.data.data
      this.pagination=data.data.pagination
      console.log(data.data.data);
      debugger
      this.media = data.data.data.map(h => h.media)
      this.images = data.data.data.map(i => i.media.image)
    }catch(err){
      console.log(err)
    }
  },
  methods: {
    pushToSingle(house){
      this.$router.push(`houses/${house.id}`)
    },
  //   getImage()
  //   {
  // let numbr = Math.random * (images.length + 1 / 100).round
  // let img = images.$;numbr.id
  // return (`${this.$config.appUrl}/api/media/${img}`)
  //   },
  },



  watch:{
    pagination(){
      //api call<
    }
  }

}
</script>

<style scoped>

</style>
