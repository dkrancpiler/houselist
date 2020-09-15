<template>
  <div>
    <h1>{{house.seo_title}}</h1>
    <span v-if="house.description == null">Information for this product is unavailable</span>
    <div v-else>
      <img v-if="images[0]" alt ="Image is unavailable" class ="image" height = "200" width ="200" v-bind:src="`${$config.apiUrl}/api/media/` + images[2].id">
      <span v-else>Images regarding this real estate cannot be shown!</span>
      <p v-if="house.description != null">{{house.description}}</p>
      <p v-else>Description about this real estate is unavailable!</p>
      <p v-if="house.address">Address of the real estate: {{house.address}}</p>
      <p v-else>Address of the real estate isn't specified!</p>
      <p v-if="house.owner">Real estate owner's phone number: {{house.owner.phones[0].number}}</p>
      <p v-else>Real estate owner's phone number isn't available.</p>
    </div>
  </div>
</template>

<script>
require('dotenv').config()
import axios from "axios"
export default {
  data() {
    return {
      house: [],
      images: []
    }
  },


  async mounted() {
    try {
      var routeid = this.$route.params.houses_id
      console.log(routeid)
      let {data} = await axios.get(`${this.$config.appUrl}/api/home/` + routeid)
      console.log(data.data);
      console.log(data.data.media.image.map(i=>i));
      debugger
      this.house = data.data
      this.images = data.data.media.image.map(i => i)
    } catch (err) {
      console.log(err)
    }
  }
}
</script>

<style scoped>

</style>
