<template>
  <div>
    <h1>POPIS KUĆA</h1>
    <template v-for="house in houses">
      <div :key="house.id">{{house.title}}
      <span v-for="index in images">
        <img class = "image" height = "200" width ="200" src="getImage()">
      </span>
      </div>
    </template>
    <pagination>

    </pagination>
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
      this.images = this.media.map(i => i.images)
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
