<template>
  <div>
    <h2>{{message}}</h2>
    <nuxt-link :to="'/flashcards'">
      <button>Go To Flashcards</button>
    </nuxt-link>
    <div class="launchWrapper">
      <nuxt-link class="launchCard" :to="`launches/${launch.flight_number}`" v-for="launch in launches" v-bind:key="launch.flight_number">
        <p>{{launch.mission_name}}</p>
        <img :src="imgSrc"/>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import rocket from '../assets/images/rocketinsights.svg'

  export default {
    data() {
      return { 
        message: 'Welcome! Here you can view all SpaceX launches!',
        launches: [],
        imgSrc: rocket
      }
    },
    methods: {
      useFetch: async function () {
        const { data } = await axios.get('https://api.spacexdata.com/v3/launches')
        this.launches = data
      }
    },
    beforeMount(){
      this.useFetch()
    }
  }
</script>

<style>
  .launchWrapper {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin: auto;
    width: 90%;
  }

  .launchCard {
    justify-content: space-evenly;
    align-content: center;
    width: 180px;
    height: 240px;
    border: 1px solid #000000;
    margin: 10px;
  }
</style>
