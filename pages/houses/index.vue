<template>
  <div>
    <h1>POPIS KUĆA</h1>
    <template v-for="house in houses">
      <div :key="house.id">{{house.title}}
      <span class = "image">
        <img height = "200" width ="200" src="http://homehapp-api.jsteam.gaussx.com/api/media/59987">
      </span>
      </div>
    </template>
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
export default {
  data(){
    return{
      houses: [],
      pagination: {}
    }
  },

  async mounted () {
    try {
      let { data } = await axios.get (`${this.$config.appUrl}/api/home`)
      this.houses=data.data.data
      this.pagination=data.data.pagination
    }catch(err){
      console.log(err)
    }
  },

  methods: {
    pushToSingle(house){
      this.$router.push(`houses/${house.id}`)
    }
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
